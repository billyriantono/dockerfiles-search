FROM confluentinc/cp-kafka-connect
MAINTAINER Bob Olde Hampsink <b.oldehampsink@nerds.company>

# Which versions?
ENV KAFKA_CONNECT_FS_VERSION 0.2

# Install Maven
RUN apt-get update -y && apt-get install -y maven

# Build kafka-connect-fs
RUN mkdir -p /tmp/quickstart/jars \
 && curl -k -SL https://github.com/mmolimar/kafka-connect-fs/archive/v$KAFKA_CONNECT_FS_VERSION.tar.gz | tar -xzf - -C /tmp/quickstart/jars --strip-components=1 \
 && cd /tmp/quickstart/jars \
 && mvn clean package \
 && mv /tmp/quickstart/jars/target /usr/share/java/kafka-connect-fs
