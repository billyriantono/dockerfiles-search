# Builds an image for Apache Kafka 0.8.1.1 from binary distribution. # # The netflixoss/java base image runs Oracle Java 8 installed atop the # ubuntu:trusty (14.04) official image. Docker's official java images are # OpenJDK-only currently, and the Kafka project, Confluent, and most other # major Java projects test and recommend Oracle Java for production for optimal # performance. 
FROM netflixoss/java:8 


# The Scala 2.11 build is currently recommended by the project. 
ENV KAFKA_VERSION=0.10.2.0 KAFKA_SCALA_VERSION=2.12 JMX_PORT=7203 
ENV KAFKA_RELEASE_ARCHIVE kafka_${KAFKA_SCALA_VERSION}-${KAFKA_VERSION}.tgz 

RUN mkdir /kafka /data /logs && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ca-certificates

# Download Kafka binary distribution 
ADD http://www.us.apache.org/dist/kafka/${KAFKA_VERSION}/${KAFKA_RELEASE_ARCHIVE} /tmp/
ADD https://dist.apache.org/repos/dist/release/kafka/${KAFKA_VERSION}/${KAFKA_RELEASE_ARCHIVE}.md5 /tmp/

WORKDIR /tmp

# Check artifact digest integrity 
# Install Kafka to /kafka 
RUN echo VERIFY CHECKSUM: && \
  gpg --print-md MD5 ${KAFKA_RELEASE_ARCHIVE} 2>/dev/null && \
  cat ${KAFKA_RELEASE_ARCHIVE}.md5 && \
  tar -zx -C /kafka --strip-components=1 -f ${KAFKA_RELEASE_ARCHIVE} && \
  rm -rf kafka_* /var/cache/apt/* /tmp/* /var/tmp/*

ADD config /kafka/config
ADD start.sh /start.sh

# Set up a user to run Kafka 
RUN useradd -u 1001 -g 0 default && \
  chown -R 1001:0 /kafka /data /logs && \
  chmod -R g+rw /kafka /data /logs

#USER kafka 
USER 1001 

ENV PATH /kafka/bin:$PATH 
WORKDIR /kafka

# broker, jmx
EXPOSE 9092  
VOLUME [ "/data", "/logs" ]

ENV ZOOKEEPER_IP zookeeper
ADD start_kafka_with_topics.sh /start2.sh
ENTRYPOINT ["/start2.sh"]
CMD ["/kafka/bin/kafka-server-start.sh", "/kafka/config/server.properties"]
