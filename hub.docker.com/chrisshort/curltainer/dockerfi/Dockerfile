FROM java:8u111-jdk-alpine

ENV KAFKA_HOME=/opt/kafka

ADD https://www-us.apache.org/dist/kafka/2.3.0/kafka_2.12-2.3.0.tgz /tmp/

RUN apk add --no-cache bash \
 && mkdir /opt \
 && tar zxf /tmp/kafka_2.12-2.3.0.tgz -C /opt \
 && ln -s /opt/kafka_2.12-2.3.0 /opt/kafka \
 && rm /tmp/*

EXPOSE 9092

CMD ["/opt/kafka/bin/kafka-server-start.sh", "/opt/kafka/config/server.properties"]
