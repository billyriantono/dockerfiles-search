FROM anapsix/alpine-java

ARG kafka_version=0.8.2.2
ARG scala_version=2.10

RUN apk add --update unzip wget curl docker jq coreutils vim net-tools

ENV KAFKA_VERSION=$kafka_version SCALA_VERSION=$scala_version
ENV KAFKA=kafka_${SCALA_VERSION}-${KAFKA_VERSION}

RUN wget -q http://apache.mirror.globo.tech/kafka/${KAFKA_VERSION}/${KAFKA}.tgz -O /tmp/${KAFKA}.tgz
RUN tar xfz /tmp/${KAFKA}.tgz -C /opt

CMD bash
