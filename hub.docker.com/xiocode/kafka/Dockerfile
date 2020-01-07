# Kafka and Zookeeper

FROM xiocode/java:7

ENV DEBIAN_FRONTEND noninteractive

# Install Kafka, Zookeeper and other needed things
RUN apt-get update && \
    apt-get install -y zookeeper wget supervisor dnsutils && \
    rm -rf /var/lib/apt/lists/* && \
    wget -q http://mirror.cc.columbia.edu/pub/software/apache/kafka/0.8.2.1/kafka_2.10-0.8.2.1.tgz -O /tmp/kafka.tgz && \
    mkdir /usr/local/kafka && \
    tar xfz /tmp/kafka.tgz -C /usr/local/kafka --strip-components=1 && \
    rm /tmp/kafka.tgz

ENV KAFKA_HOME /usr/local/kafka
ADD scripts/start-kafka.sh /usr/bin/start-kafka.sh

# Supervisor config
ADD supervisor/kafka.conf /etc/supervisor/conf.d/kafka.conf

# KAFKA config

VOLUME ["/usr/local/kafka/config","/usr/local/kafka/logs", "/var/lib/kafka"]

# 9092 is kafka
EXPOSE 9092

CMD ["supervisord", "-n"]
