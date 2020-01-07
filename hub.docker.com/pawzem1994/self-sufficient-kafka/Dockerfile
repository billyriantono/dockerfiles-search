# Kafka and Zookeeper

FROM adoptopenjdk:11-jre-hotspot

ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 2.3.1
ENV KAFKA_HOME /opt/kafka/bin
ENV KAFKA_UNPACK_LOCATION /opt/kafka_2.11-2.3.1
ENV SERVER_PROPERTIES configs/server.properties

RUN apt-get update
RUN apt-get install -y supervisor
RUN apt-get install -y zookeeper

ADD resources/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz /opt
RUN mv $KAFKA_UNPACK_LOCATION /opt/kafka

ADD $SERVER_PROPERTIES /opt/configs/

ADD supervisor/zookeeper.conf /etc/supervisor/conf.d/
ADD supervisor/kafka.conf /etc/supervisor/conf.d/

#RUN /usr/share/zookeeper/bin/zkServer.sh start-foreground
#RUN /opt/kafka/bin/kafka-server-start.sh /opt/configs/server.properties

# 2181 is zookeeper, 9092 is kafka
EXPOSE 2181 9092

CMD ["supervisord", "-n"]
