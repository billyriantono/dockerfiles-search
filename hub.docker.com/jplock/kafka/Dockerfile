# DOCKER-VERSION 1.1.2
# VERSION        0.1

FROM debian:jessie
MAINTAINER Justin Plock <justin@plock.net>

RUN apt-get update && apt-get install -y openjdk-7-jre-headless wget
RUN wget -q -O - http://mirror.cogentco.com/pub/apache/kafka/0.8.1.1/kafka_2.10-0.8.1.1.tgz | tar -xzf - -C /opt

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
ENV KAFKA_HOME /opt/kafka_2.10-0.8.1.1

WORKDIR /opt/kafka_2.10-0.8.1.1

VOLUME ["/tmp/kafka-logs", "/opt/kafka_2.10-0.8.1.1"]

EXPOSE 9092

ENTRYPOINT ["bin/kafka-server-start.sh"]
CMD ["config/server.properties"]
