FROM ubuntu:16.04

ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 0.10.0.1
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

RUN apt-get update \
	&& apt-get install -y \
	tar \
	supervisor \
	openjdk-8-jre-headless \
	wget

RUN apt-get clean \
	&& rm -rf /var/lib/apt/lists/* \
	 /tmp/* \
	 /var/tmp/*

RUN wget -q http://mirror.fibergrid.in/apache/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz \
	-O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz \
	&& tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt

RUN ln -s $KAFKA_HOME /opt/kafka

WORKDIR	$KAFKA_HOME

ADD supervisor/kafka.conf supervisor/zookeeper.conf /etc/supervisor/conf.d/
ADD script/start.sh /opt/

EXPOSE 2181 9092

CMD ["/opt/start.sh"]
