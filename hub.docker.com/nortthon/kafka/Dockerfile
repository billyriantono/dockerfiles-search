FROM java:8
MAINTAINER  Lucas Augusto <nortthon@gmail.com>

RUN \
  wget http://www-eu.apache.org/dist/kafka/0.10.2.0/kafka_2.11-0.10.2.0.tgz ;\
  tar -xzf kafka_2.11-0.10.2.0.tgz

ADD start-kafka.sh .

EXPOSE 2181
EXPOSE 9092

CMD ["/bin/bash", "start-kafka.sh"]
