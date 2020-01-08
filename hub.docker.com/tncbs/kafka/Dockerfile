FROM adoptopenjdk/openjdk11:x86_64-alpine-jre-11.0.5_10

ARG kafka_version=2.4.0
ARG scala_version=2.13
ARG vcs_ref=unspecified
ARG build_date=unspecified

LABEL org.opencontainers.image.authors="jiraphon.sa <jiraphon.sa@tnis.com>" \
    org.opencontainers.image.name="kafka" \
    org.opencontainers.image.description="Apache Kafka" \
    org.opencontainers.image.created="${build_date}" \
    org.opencontainers.image.revision="${vcs_ref}" \
    org.opencontainers.image.url-ref="https://github.com/wurstmeister/kafka-docker" \
    org.opencontainers.image.version="${scala_version}_${kafka_version}" \
    org.opencontainers.image.vendor="T.N. Incorporation Ltd."

ENV KAFKA_VERSION=$kafka_version \
    SCALA_VERSION=$scala_version \
    KAFKA_HOME=/opt/kafka

ENV PATH=${PATH}:${KAFKA_HOME}/bin

COPY kafka/download-kafka.sh \
    kafka/start-kafka.sh \
    kafka/broker-list.sh \
    kafka/create-topics.sh \
    kafka/versions.sh /tmp/

RUN apk add --no-cache bash curl jq docker \
 && chmod a+x /tmp/*.sh \
 && mv /tmp/start-kafka.sh /tmp/broker-list.sh /tmp/create-topics.sh /tmp/versions.sh /usr/bin \
 && sync && /tmp/download-kafka.sh \
 && tar xfz /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt \
 && rm /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz \
 && ln -s /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION} ${KAFKA_HOME} \
 && rm /tmp/*

COPY kafka/overrides /opt/overrides

VOLUME ["/kafka"]

# Use "exec" form so that it runs as PID 1 (useful for graceful shutdown)
CMD ["start-kafka.sh"]
