FROM openjdk:7

MAINTAINER Leandro Pineda

ENV KAFKA_VERSION="0.10.1.0" SCALA_VERSION="2.11" KAFKA_HOME="/kafka"
ADD download-kafka.sh /tmp/download-kafka.sh
ADD start-kafka.sh /usr/sbin/start-kafka.sh

ENV ZOO_CONN="localhost" ZOO_PORT="2181"

EXPOSE 9092

RUN apt-get update && \
	apt-get install -y jq

RUN chmod a+x /usr/sbin/start-kafka.sh && \
	chmod a+x /tmp/download-kafka.sh && \
	/bin/bash /tmp/download-kafka.sh && \
	tar -xzf /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz --directory / && \
	mv /kafka_${SCALA_VERSION}-${KAFKA_VERSION} ${KAFKA_HOME} && \
	rm /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz 


WORKDIR ${KAFKA_HOME}

# start-kafka.sh replace the zookeeper.connection value with those in $ZOO_CONN and $ZOO_PORT a then runs kafka.
CMD ["/bin/bash", "/usr/sbin/start-kafka.sh"]
