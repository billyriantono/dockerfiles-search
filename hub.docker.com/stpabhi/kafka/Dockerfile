FROM centos:6.6

MAINTAINER "Abhilash S T P"

RUN yum -y update; yum install -y vim unzip tar untar wget epel-release
RUN yum --enablerepo=epel -y install docker-io

RUN wget -q --no-check-certificate --no-cookies --header 'Cookie: oraclelicense=accept-securebackup-cookie' http://download.oracle.com/otn-pub/java/jdk/7u75-b13/jdk-7u75-linux-x64.tar.gz -O /tmp/jdk-7u75-linux-x64.tar.gz
RUN tar zxf /tmp/jdk-7u75-linux-x64.tar.gz -C /opt

ENV JAVA_HOME /opt/jdk1.7.0_75

RUN wget -q http://download.nextag.com/apache/kafka/0.8.2.1/kafka_2.10-0.8.2.1.tgz -O /tmp/kafka_2.10-0.8.2.1.tgz
RUN tar xfz /tmp/kafka_2.10-0.8.2.1.tgz -C /opt

VOLUME ["/kafka"]

EXPOSE 9092

ENV KAFKA_HOME /opt/kafka_2.10-0.8.2.1
ADD start-kafka.sh /usr/bin/start-kafka.sh
CMD start-kafka.sh
