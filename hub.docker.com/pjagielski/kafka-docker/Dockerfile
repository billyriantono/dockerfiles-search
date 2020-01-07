FROM ubuntu

MAINTAINER touk

RUN echo "deb http://archive.ubuntu.com/ubuntu precise universe" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y unzip  openjdk-6-jdk wget

RUN wget https://people.apache.org/~joestein/kafka-0.8.1-candidate2/kafka_2.10-0.8.1.tgz -P /tmp
RUN ls /tmp
RUN tar xfz /tmp/kafka_2.10-0.8.1.tgz -C /opt

ENV KAFKA_HOME /opt/kafka_2.10-0.8.1

EXPOSE 2181 2888 3888 9092

ADD start-kafka.sh /usr/bin/start-kafka.sh 
CMD start-kafka.sh 
