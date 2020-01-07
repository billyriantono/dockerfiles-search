FROM openjdk:11-jre

ENV KAFKA_VERSION=2.3.1
EXPOSE 9092

ADD entrypoint.sh /entrypoint.sh

RUN wget https://archive.apache.org/dist/kafka/$KAFKA_VERSION/kafka_2.12-$KAFKA_VERSION.tgz \
    && tar -xzf kafka_2.12-$KAFKA_VERSION.tgz \
    && rm -rf kafka_2.12-$KAFKA_VERSION.tgz \
    && mv kafka_2.12-$KAFKA_VERSION /usr/local/kafka \
    && chmod +x /entrypoint.sh 

ENTRYPOINT ["/entrypoint.sh"]