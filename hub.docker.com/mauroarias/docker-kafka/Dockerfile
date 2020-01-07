FROM mauroarias/docker-java8_debian

MAINTAINER Mauro Arias <mauro.arias.a@gmail.com>

ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 0.10.1.1
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"
ENV ZOOKEEPER_PORT 2181
ENV KAFKA_PORT 9092

RUN apt-get update && \
    apt-get install -y zookeeper wget supervisor dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar -vzxf kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    apt-get -y remove wget && \
    apt-get clean all

ADD start-kafka.sh /usr/bin/start-kafka.sh
ADD supervisor_kafka.conf supervisor_zookeeper.conf /etc/supervisor/conf.d/

EXPOSE $ZOOKEEPER_PORT $KAFKA_PORT

CMD ["supervisord", "-n"]
