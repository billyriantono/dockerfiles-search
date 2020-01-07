FROM openjdk:8-jre-alpine

MAINTAINER Naren <nanichowdary.ravilla@gmail.com>

ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 1.0.2
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"
ENV ZK_HOME /opt/zookeeper-3.4.10

RUN echo "ipv6" >> /etc/modules && \
	apk add wget && \
	apk add tar && \
	apk add --no-cache bash && \
	mkdir /opt

RUN wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    wget -q http://www-eu.apache.org/dist/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz -O /tmp/zookeeper-3.4.10.tar.gz && \
	tar xfz /tmp/zookeeper-3.4.10.tar.gz -C /opt && \
    rm /tmp/zookeeper-3.4.10.tar.gz

ADD scripts/server.properties $KAFKA_HOME/config/server.properties
ADD scripts/start-kafka.sh /start-kafka.sh

RUN chmod +x /start-kafka.sh

EXPOSE 9092

ENTRYPOINT ["/start-kafka.sh"]