FROM java:openjdk-8-jre

ARG ZOOKEEPER_VERSION
ARG SCALA_VERSION
ARG KAFKA_VERSION

ENV DEBIAN_FRONTEND=noninteractive \
    ZOOKEEPER_HOME=/opt/zookeeper-${ZOOKEEPER_VERSION} \
    KAFKA_HOME=/opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION} \
    ADVERTISED_HOST=127.0.0.1 \
    ADVERTISED_PORT=9092

RUN apt-get update \
 && apt-get install -y curl supervisor \
 && rm -rf /var/lib/apt/lists/* \
 && apt-get clean \
 && curl -sSL http://ftp.cixug.es/apache/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz | tar xz -C /opt \
 && curl -sSL https://archive.apache.org/dist/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz | tar xz -C /opt

COPY assets/conf/zoo.cfg ${ZOOKEEPER_HOME}/conf
COPY assets/scripts/* /usr/local/bin/
COPY assets/supervisor/* /etc/supervisor/conf.d/

EXPOSE 2181 ${ADVERTISED_PORT}

CMD ["supervisord", "-n"]