FROM alpine:3.5

EXPOSE 7000 7001 7199 9042 9160

ARG APK_CACHE_IP=172.17.0.1
ARG APK_CACHE_DOMAIN='dl-cdn.alpinelinux.org'

ARG RUN_DEPS='su-exec openjdk8-jre openssl bash'
ARG BUILD_DEPS='tar coreutils'

ARG CASSANDRA_VERSION=3.9
ARG CASSANDRA_URL='http://artfiles.org/apache.org/cassandra'

ENV CASSANDRA_HOME=/opt/cassandra
ENV CASSANDRA_CONF=$CASSANDRA_HOME/conf
ENV PATH=$CASSANDRA_HOME/bin:$PATH

ENV CASSANDRA_START_RPC=true

RUN nc -z $APK_CACHE_IP 80 && echo $APK_CACHE_IP $APK_CACHE_DOMAIN >>/etc/hosts \
  ; apk --update add --no-cache $RUN_DEPS $BUILD_DEPS \
    && mkdir -p $CASSANDRA_HOME/data $CASSANDRA_HOME/logs $CASSANDRA_HOME/commitlog \
    && cd $CASSANDRA_HOME \
    && CASSANDRA_LATEST=$(wget -qO- $CASSANDRA_URL | egrep -o "[0-9]+\.[0-9]+" | sort -Vr | head -1) \
    && : ${CASSANDRA_VERSION:=$CASSANDRA_LATEST} \
    && wget -O- $CASSANDRA_URL/${CASSANDRA_VERSION}/apache-cassandra-${CASSANDRA_VERSION}-bin.tar.gz | tar xz --strip-components=1 \
    && sed -i 's|^start_rpc:.*$|start_rpc: true|' $CASSANDRA_CONF/cassandra.yaml \
#    && sed -i 's|^listen_address:.*$|listen_address: localhost|' $CASSANDRA_CONF/cassandra.yaml \
    && adduser -DH -s /sbin/nologin cassandra && chown -R cassandra:cassandra $CASSANDRA_HOME \
  && apk del $BUILD_DEPS && rm -rf /var/cache/apk/*

WORKDIR $CASSANDRA_HOME

ADD . .

VOLUME $CASSANDRA_HOME/data $CASSANDRA_HOME/logs $CASSANDRA_HOME/commitlog /tmp

CMD ["su-exec", "cassandra", "cassandra", "-f"]
