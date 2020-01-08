FROM anapsix/alpine-java

MAINTAINER Ricardo Bravo <rbravo@datiobd.com>

RUN apk add --update unzip wget curl docker jq coreutils

ENV KAFKA_VERSION="0.9.0.1" SCALA_VERSION="2.11"

RUN  wget -q http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -O /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
     tar xfz /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz -C /opt && \
     rm /tmp/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz

VOLUME ["/kafka"]

ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}
ADD start-kafka.sh /usr/bin/start-kafka.sh

CMD ["start-kafka.sh"]
