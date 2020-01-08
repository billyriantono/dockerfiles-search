FROM alpine:3.5

EXPOSE 5601

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS='su-exec openjdk8-jre openssl bash nodejs'
ARG BUILD_DEPS='tar coreutils'

#ARG KIBANA_VERSION=5.1.1
ARG KIBANA_TAGS='https://api.github.com/repos/elastic/kibana/tags'
ARG KIBANA_URL='https://artifacts.elastic.co/downloads/kibana'

ENV KIBANA_HOME=/opt/kibana
ENV PATH=$KIBANA_HOME/bin:$PATH

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && mkdir -p $KIBANA_HOME && cd $KIBANA_HOME \
    && KIBANA_LATEST=$(wget -qO- $KIBANA_TAGS | egrep -o "[0-9]+\.[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && wget -O- $KIBANA_URL/kibana-${KIBANA_VERSION:=$KIBANA_LATEST}-linux-x86_64.tar.gz | tar xz --strip-components=1 \
    && rm -rf node && mkdir -p node/bin && ln -s $(which node) node/bin/node \
    && adduser -DH -s /sbin/nologin kibana && chown -R kibana:kibana $KIBANA_HOME \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR $KIBANA_HOME

ADD . .

VOLUME $KIBANA_HOME/optimize $KIBANA_HOME/data

CMD ["su-exec","kibana","kibana"]
