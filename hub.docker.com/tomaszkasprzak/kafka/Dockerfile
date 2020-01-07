FROM tomaszkasprzak/java:openjdk-8-centos

MAINTAINER Tomasz Kasprzak <tomasz.kasprzak.dev@gmail.com> 

ENV KAFKA_VERSION 2.0.0
ENV SCALA_VERSION 2.11
ENV PATH "$PATH:/opt/kafka/bin"

RUN yum update -y && \
    wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka.tgz && \
    mkdir -p /opt/kafka && \
    tar xfz /tmp/kafka.tgz --strip 1 --directory /opt/kafka && \
    rm -rf ~/tmp/kafka.tgz

EXPOSE 9092 
EXPOSE 2181

ADD ./zookeeper.conf /etc/supervisord.d/
ADD ./kafka.conf /etc/supervisord.d/

CMD ["supervisord", "-n"]