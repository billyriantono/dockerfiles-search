FROM stackbrew/ubuntu:14.04

MAINTAINER jmarsh.ext "jmarsh.ext@aviatainc.com"

ENV KAFKA_VERSION="0.8.2.1" SCALA_VERSION="2.10"

RUN apt-get update && apt-get install -y unzip openjdk-6-jdk wget curl git docker.io jq

ADD scripts/download-kafka.sh /tmp/download-kafka.sh
RUN /tmp/download-kafka.sh
RUN tar xf /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt

VOLUME ["/kafka"]

ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}
COPY scripts/start-kafka.sh /usr/bin/start-kafka.sh
COPY scripts/broker-list.sh /usr/bin/broker-list.sh
COPY scripts/create-topic-start-kafka.sh /usr/bin/create-topic-start-kafka.sh
RUN chmod +x /usr/bin/create-topic-start-kafka.sh
RUN PATH=$PATH:/opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/bin
COPY resources/server.properties /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/config/server.properties
COPY resources/consumer.properties /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/config/consumer.properties

#RUN sudo env "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/opt/mystuff/jdk1.7.0_67/bin:/opt/mystuff/storm-0.9.0.1/bin:/opt/mystuff/scala-2.10.4/bin:/opt/mystuff/sbt/bin:/opt/mystuff/kafka_2.10-0.8.1/bin:/opt/mystuff/zookeeper-3.3.6/bin:/opt/mystuff/scala-2.10.4/bin" "JAVA_HOME=/opt/mystuff/jdk1.7.0_67" "KAFKA_HOME=/opt/mystuff/kafka_2.10-0.8.1" "ZOOKEEPER_HOME=/opt/mystuff/zookeeper-3.3.6" "SCALA_HOME=/opt/mystuff/scala-2.10.4" /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/bin/kafka-topics.sh --create --zookeeper zookeeper:2181 --replication-factor 1 --partitions 1 --topic Registration
#COPY resources/server.properties /opt/server.properties
CMD create-topic-start-kafka.sh
