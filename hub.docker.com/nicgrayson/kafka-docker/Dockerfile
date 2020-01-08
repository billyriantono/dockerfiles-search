FROM anapsix/alpine-java

MAINTAINER Nic Grayson <nicgrayson@gmail.com

RUN apk add --update wget unzip

ENV KAFKA_VERSION 0.9.0.0
ENV SCALA_VERSION 2.11

RUN wget -q https://archive.apache.org/dist/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz \
  -O /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz && \
  tar xfz /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt && \
  rm /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

VOLUME ["/kafka"]

ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}

RUN chmod 755 $KAFKA_HOME/bin/*

WORKDIR /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}/bin

CMD ["ls", "-lah"]
