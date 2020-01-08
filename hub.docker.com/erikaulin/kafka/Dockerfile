FROM anapsix/alpine-java
MAINTAINER Erik Aulin <erik.aulin@zook.ai>

RUN apk add --update unzip wget curl docker jq coreutils tar

# Set the version, home directory, and MD5 hash.
# MD5 hash taken from http://kafka.apache.org/downloads.html for this version of Kafka
ENV KAFKA_VERSION="0.10.0.0" \
    SCALA_VERSION="2.11" \
    KAFKA_HOME=/kafka \
    MD5HASH=F6A887BA61341071EC26C392C2A5D363

# Create directory for Kafka
RUN mkdir $KAFKA_HOME && \
    mkdir $KAFKA_HOME/data && \
    mkdir $KAFKA_HOME/logs

# Download Kafka
RUN curl -fSL -o /tmp/kafka.tgz $(curl --stderr /dev/null https://www.apache.org/dyn/closer.cgi\?as_json\=1 | sed -rn 's/.*"preferred":.*"(.*)"/\1/p')kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz

# Verify the contents and then install ...
RUN echo "$MD5HASH  /tmp/kafka.tgz" | md5sum -c - &&\
    tar xzf /tmp/kafka.tgz -C $KAFKA_HOME --strip-components=1 &&\
    rm -f /tmp/kafka.tgz

COPY ./log4j.properties $KAFKA_HOME/config/log4j.properties

# Set the working directory to the Kafka home directory
WORKDIR $KAFKA_HOME

# Expose the ports and set up volumes for the data and logs directories
EXPOSE 9092
VOLUME ["/kafka/data","/kafka/logs","/kafka/config"]

ADD docker-entrypoint.sh /usr/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/bin/docker-entrypoint.sh"]
CMD ["start"]
