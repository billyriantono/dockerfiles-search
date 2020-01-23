FROM alpine:3.5

EXPOSE 9200 9300

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS='su-exec openjdk8-jre openssl bash'
ARG BUILD_DEPS='tar coreutils'

#ARG ES_VERSION=5.1.1
ARG ES_TAGS='https://api.github.com/repos/elastic/elasticsearch/tags'
ARG ES_URL='https://artifacts.elastic.co/downloads/elasticsearch'

ENV ES_HOME=/opt/elasticsearch
ENV PATH=$ES_HOME/bin:$PATH

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && mkdir -p $ES_HOME && cd $ES_HOME \
    && ES_LATEST=$(wget -qO- $ES_TAGS | egrep -o "[0-9]+\.[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && wget -O- $ES_URL/elasticsearch-${ES_VERSION:=$ES_LATEST}.tar.gz | tar xz --strip-components=1 \
    && bin/elasticsearch-plugin install repository-s3 \
    && mkdir data logs config/scripts \
    && adduser -DH -s /sbin/nologin elasticsearch && chown -R elasticsearch:elasticsearch $ES_HOME \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR $ES_HOME

ADD . .

VOLUME $ES_HOME/data $ES_HOME/logs /tmp

ENTRYPOINT ["su-exec","elasticsearch","elasticsearch"]
