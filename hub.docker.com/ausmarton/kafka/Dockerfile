FROM openjdk:jre-slim

WORKDIR /root
USER root

ENV KAFKA_VERSION 1.0.0
ENV SCALA_VERSION 2.12
ENV KAFKA_HOME kafka_$SCALA_VERSION-$KAFKA_VERSION

ADD https://archive.apache.org/dist/kafka/$KAFKA_VERSION/$KAFKA_HOME.tgz $KAFKA_HOME.tgz
RUN tar -xzf $KAFKA_HOME.tgz

ENV BROKER localhost
ENV TOPIC sample
ENV PORT 9092

CMD ./$KAFKA_HOME/bin/kafka-console-consumer.sh --bootstrap-server $BROKER:$PORT --topic $TOPIC
