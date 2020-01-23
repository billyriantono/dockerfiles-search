FROM java:7
MAINTAINER Binh Van Nguyen

ENV KAFKA_HOME /opt/kafka
ENV KAFKA_VERSION 0.8.2.0
ENV SCALA_VERSION 2.10

WORKDIR $KAFKA_HOME
RUN curl -L http://apache.mirrors.tds.net/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz | tar -xzC $KAFKA_HOME --strip-components=1

ENTRYPOINT ["bin/entrypoint.sh"]
COPY entrypoint.sh bin/entrypoint.sh
RUN chmod +x bin/entrypoint.sh