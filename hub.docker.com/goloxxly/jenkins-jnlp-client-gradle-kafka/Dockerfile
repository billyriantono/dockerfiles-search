FROM goloxxly/jenkins-jnlp-client-gradle:3.1.0

ENV SCALA_VERSION 2.12
ENV KAFKA_VERSION 0.10.2.1
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka, Zookeeper and other needed things
RUN curl http://apache.mirror.anlx.net/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz | tar -xz -C /opt

COPY extended-start.sh /usr/local/bin/extended-start.sh
RUN chmod +x /usr/local/bin/extended-start.sh

ENTRYPOINT ["/usr/local/bin/extended-start.sh"]
