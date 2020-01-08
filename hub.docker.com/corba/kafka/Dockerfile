FROM ubuntu:16.04
MAINTAINER Cornel


ENV DEBIAN_FRONTEND noninteractive
ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 0.10.0.0
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper and other needed things
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" > /etc/apt/sources.list.d/webupd8team-java.list \
    && echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" >> /etc/apt/sources.list.d/webupd8team-java.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886 \
    && apt-get -y update \
    && echo debconf shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
    && apt-get -y install oracle-java8-installer oracle-java8-set-default \
    && apt-get -y install supervisor \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz \
    && tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt \
    && rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

COPY scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
COPY supervisor/kafka.conf /etc/supervisor/conf.d/

ENV ZOOKEEPER_HOST zookeeper
ENV ZOOKEEPER_PORT 2181 
ENV ZOOKEEPER_CHROOT kafka

# 9092 is kafka
EXPOSE 9092

CMD ["supervisord", "-n"]

