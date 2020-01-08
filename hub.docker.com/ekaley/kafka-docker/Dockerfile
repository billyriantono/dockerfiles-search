FROM openjdk:8u131-jdk-alpine

MAINTAINER Ethan Kaley <ethan.kaley@dell.com>

ENV ZK_HOSTS=localhost:2181 \
    KM_VERSION=1.3.3.14 \
    KM_REVISION=5de818f330365fc3cd835b8227875ad12f29ed15 \
    KM_CONFIGFILE="conf/application.conf" \
    KM_USERNAME=admin \
    KM_PASSWORD=admin

ADD start-kafka-manager.sh /kafka-manager-${KM_VERSION}/start-kafka-manager.sh

RUN apk --no-cache add --virtual build-deps git wget unzip bash && \
    mkdir -p /tmp && \
    cd /tmp && \
    git clone https://github.com/yahoo/kafka-manager && \
    cd /tmp/kafka-manager && \
    git checkout ${KM_REVISION} && \
    echo 'scalacOptions ++= Seq("-Xmax-classfile-name", "200")' >> build.sbt && \
    ./sbt clean dist && \
    unzip -d / ./target/universal/kafka-manager-${KM_VERSION}.zip && \
    rm -rf /tmp/* /root/.sbt /root/.ivy2 && \
    chmod +x /kafka-manager-${KM_VERSION}/start-kafka-manager.sh && \
    rm -rf /kafka-manager-${KM_VERSION}/share && \
    apk del git wget unzip

WORKDIR /kafka-manager-${KM_VERSION}

EXPOSE 9000
ENTRYPOINT ["./start-kafka-manager.sh"]
