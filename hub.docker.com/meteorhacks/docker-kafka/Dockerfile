FROM dockerfile/java:oracle-java8
MAINTAINER Meteorhacks

RUN wget -q -O - http://www.interior-dsgn.com/apache/kafka/0.8.2.1/kafka_2.11-0.8.2.1.tgz | tar -xzf - -C /opt \
    && mv /opt/kafka_2.11-0.8.2.1 /opt/kafka

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

EXPOSE 9092 7203

VOLUME ["/opt/kafka/config/server.properties", "/tmp/kafka-logs"]

WORKDIR /opt/kafka/bin
ENTRYPOINT ["./kafka-server-start.sh"]
CMD ["../config/server.properties"]
