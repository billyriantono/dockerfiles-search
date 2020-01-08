FROM openjdk:8-jre-alpine

ARG MIRROR=http://www-eu.apache.org/dist

ENV KAFKA_VERSION=0.9.0.1 \
    KAFKA_HOME=/opt/kafka \
    SCALA_VERSION=2.11

LABEL name="kafka" \
      kafka_version=$KAFKA_VERSION \
      scala_version=$SCALA_VERSION

RUN apk add --no-cache \
      bash \
      curl \
      ruby && \
    mkdir /opt && \
    curl -f ${MIRROR}/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz | tar -xzf - -C /tmp && \
    mv /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION} ${KAFKA_HOME} && \
    mv ${KAFKA_HOME}/config ${KAFKA_HOME}/config.dist && \
    mkdir -p ${KAFKA_HOME}/config && \
    cp ${KAFKA_HOME}/config.dist/log4j.properties ${KAFKA_HOME}/config && \
    cp ${KAFKA_HOME}/config.dist/tools-log4j.properties ${KAFKA_HOME}/config

COPY ["configure-and-run-server.rb", "/opt/kafka/bin/"]

WORKDIR $KAFKA_HOME

CMD ["/opt/kafka/bin/configure-and-run-server.rb", "/opt/kafka/config/server.properties"]
