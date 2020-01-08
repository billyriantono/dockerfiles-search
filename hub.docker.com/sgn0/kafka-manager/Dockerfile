FROM sgn0/java
MAINTAINER Jesus Lopez <jesus@sgn.com>

ENV KAFKA_MANAGER_VERSION=1.3.0.8

RUN set -ex; \
    apk --no-cache -fqt .deps add bash openjdk8 nodejs wget; \
    mkdir -p /usr/src; \
    wget -qO- https://github.com/jlopez/kafka-manager/archive/master.tar.gz | \
        tar xzf - -C/usr/src; \
    cd /usr/src/kafka-manager-master; \
    echo 'scalacOptions ++= Seq("-Xmax-classfile-name", "200")' >> build.sbt; \
    ./sbt clean dist; \
    mkdir /opt; \
    unzip -d /opt target/universal/kafka-manager-${KAFKA_MANAGER_VERSION}.zip; \
    cd /; \
    rm -fr /tmp/* /root/.sbt /root/.ivy2 /usr/src/kafka-manager-${KAFKA_MANAGER_VERSION}; \
    apk --no-cache -q del .deps; \
    apk --no-cache -q add bash

COPY kafka-manager /usr/bin/kafka-manager

CMD ["/usr/bin/kafka-manager"]
