FROM openjdk:8u151-jre-alpine
MAINTAINER Alexandre Lepretre <alexandre.lprtr@gmail.com>

# fixed, informational ENV vars:
# for Kafka
ENV KAFKA_VERSION="0.11.0.3"
ENV SCALA_VERSION="2.12"
ENV KAFKA_HOME=/opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}
ENV KAFKA_BROKER_ID="-1"
ENV START_TIMEOUT="600"
ENV KAFKA_PORT="9092"
ENV KAFKA_ZOOKEEPER_PORT="2181"
ENV GLIBC_VERSION="2.27-r0"

# for ZK
ENV ZOOKEEPER_VERSION="3.4.13"
ENV ZK_HOME="/opt/zookeeper-${ZOOKEEPER_VERSION}"


# Kafka runtime config, may be overridden:
ENV KAFKA_ADVERTISED_PORT="9092"
ENV KAFKA_ADVERTISED_HOST_NAME="localhost"
ENV KAFKA_HEAP_OPTS=""
ENV KAFKA_LOG_DIRS="/kafka/kafka-logs-$HOSTNAME"
ENV KAFKA_ZOOKEEPER_CONNECT="localhost:2181"

# Install Kafka
ADD http://www-eu.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz /tmp/kafka.tgz
RUN mkdir /opt/ && \
    tar xfz /tmp/kafka.tgz -C /opt/ && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk && \
    apk add --no-cache --allow-untrusted glibc-${GLIBC_VERSION}.apk && \
    rm glibc-${GLIBC_VERSION}.apk && \
    rm /tmp/kafka.tgz

# Install ZK
ADD http://mirror.vorboss.net/apache/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz /tmp/zookeeper.tar.gz
RUN tar -xzf /tmp/zookeeper.tar.gz -C /opt/ && \
    rm /tmp/zookeeper.tar.gz && \
    mv /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo_sample.cfg /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo.cfg && \
    sed  -i "s|/tmp/zookeeper|$ZK_HOME/data|g" $ZK_HOME/conf/zoo.cfg; mkdir $ZK_HOME/data

# net-tools needed for create-topics.sh
RUN apk update && apk add net-tools bash

ADD start-kafka.sh /usr/bin/start-kafka.sh
# TODO not really sure if this is needed, Kafka is running in auto create topic anyway!
ADD create-topics.sh /usr/bin/create-topics.sh

EXPOSE 2181 2888 3888
EXPOSE 9092

VOLUME [ "/kafka", "${ZK_HOME}/conf", "${ZK_HOME}/data" ]

# Use "exec" form so that it runs as PID 1 (useful for graceful shutdown)
CMD ["start-kafka.sh"]
