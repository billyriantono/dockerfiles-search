FROM centos
RUN mkdir -p /opt/kafka \
  && cd /opt/kafka \
  && yum -y install java-1.8.0-openjdk-headless tar \
  && curl -s http://mirrors.hostingromania.ro/apache.org/kafka/1.1.0/kafka-1.1.0-src.tgz | tar -xz --strip-components=1 \
  && yum clean all
RUN chmod -R g=u /opt/kafka
WORKDIR /opt/kafka
VOLUME /tmp/kafka-logs /tmp/zookeeper
EXPOSE 2181 2888 3888 9092
