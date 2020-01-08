FROM centos:centos7

ENV SCALA_VERSION 2.11
ENV KAFKA_VERSION 0.10.1.1
ENV KAFKA_HOME /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"

# Install Kafka
RUN yum upgrade -y && \
    yum install -y java-1.8.0-openjdk && \
    yum install -y https://archive.cloudera.com/cdh5/one-click-install/redhat/7/x86_64/cloudera-cdh-5-0.x86_64.rpm && \
    yum install -y zookeeper && \
    curl http://apache.mirrors.spacedump.net/kafka/"$KAFKA_VERSION"/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -o /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz && \
    tar xfz /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz -C /opt && \
    rm /tmp/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION".tgz

RUN ln -s /opt/kafka_"$SCALA_VERSION"-"$KAFKA_VERSION"/bin/*.sh /usr/bin/
