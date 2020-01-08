FROM aviata/ubuntu

#Kafka 0.8.1.1

#install
RUN date -u +"%Y-%m-%d %H:%M%S?" && wget apache.mirrors.spacedump.net/kafka/0.8.1.1/kafka_2.8.0-0.8.1.1.tgz -O /tmp/kafka_2.8.0-0.8.1.1.tgz \
    && date -u +"%Y-%m-%d %H:%M%S?" && tar xfz /tmp/kafka_2.8.0-0.8.1.1.tgz -C /opt \
    && date -u +"%Y-%m-%d %H:%M%S?" && rm /tmp/kafka_2.8.0-0.8.1.1.tgz

EXPOSE 9092

VOLUME ["/opt/kafka"]
