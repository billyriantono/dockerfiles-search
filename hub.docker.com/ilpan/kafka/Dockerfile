FROM ilpan/jdk:8-alpine3.8

LABEL maintainer=ilpan:<pna.dev@outlook.com>

ENV KAFKA_HOME=/spark \
    KAFKA_VERSION=2.0.1 \
    SCALA_VERSION=2.11 \
    MIRROR=https://archive.apache.org/dist/

ENV PATH=${PATH}:${KAFKA_HOME}/bin \
    KAFKA_DOWURL=${MIRROR}/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

RUN \
    cd /tmp \
    && wget -qc ${KAFKA_DOWURL} -O kafka.tgz \
    && mkdir -p ${KAFKA_HOME} \
    && tar -xzf kafka.tgz -C ${KAFKA_HOME} --strip-components=1 \
    && rm -rf /tmp/*

WORKDIR ${KAFKA_HOME}

COPY ./docker-entrypoint.sh ./

ENTRYPOINT [ "./docker-entrypoint.sh" ]