FROM srakshit/alpine-base

MAINTAINER Subham Rakshit

ENV KAFKA_HOME="/opt/kafka" \
    KAFKA_VERSION="0.10.2.0" \
    SCALA_VERSION="2.10" \
    PATH=$PATH:$KAFKA_HOME/bin

ADD ./kafka-* /opt/

RUN chmod +x /opt/kafka-download.sh \
    && sleep 1 \
    && /opt/kafka-download.sh \
    && rm /opt/kafka-download.sh \
    && ln -s /opt/kafka_$SCALA_VERSION-$KAFKA_VERSION $KAFKA_HOME \
    && addgroup kafka \
    && adduser -S -G kafka kafka \
    && chown kafka:kafka -R /opt/kafka* \
    && chmod 754 /opt/kafka*
