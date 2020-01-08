FROM alpine

EXPOSE 9600 12201

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS='su-exec openjdk8-jre openssl bash libzmq'
ARG BUILD_DEPS='tar coreutils'

#ARG LS_VERSION=5.1.1
ARG LS_TAGS='https://www.elastic.co/downloads/logstash'
ARG LS_URL='https://artifacts.elastic.co/downloads/logstash'

ENV LS_HOME=/opt/logstash
ENV LS_SETTINGS_DIR=$LS_HOME/config
ENV PATH=$LS_HOME/bin:$PATH

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && mkdir -p $LS_HOME && cd $LS_HOME \
    && LS_LATEST=$(wget -qO- $LS_TAGS | egrep -o "[0-9]+\.[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && echo "Installing Logstash ${LS_VERSION:=$LS_LATEST}" \
    && wget -O- $LS_URL/logstash-${LS_VERSION}.tar.gz | tar xz --strip-components=1 \
    && bin/logstash-plugin install logstash-input-gelf \
    && bin/logstash-plugin install logstash-input-s3 \
    && bin/logstash-plugin install logstash-input-sqs \
    && bin/logstash-plugin install logstash-output-graphite \
    && adduser -DH -s /sbin/nologin logstash && chown -R logstash:logstash $LS_HOME \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR $LS_HOME 

ADD . .

#VOLUME $LS_HOME/logs

ENTRYPOINT ["su-exec","logstash","logstash"]

CMD ["-e"]
