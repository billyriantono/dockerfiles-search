FROM ubuntu:14.04
MAINTAINER Olivier Devoisin <devoxi.git@outlook.com>

RUN apt-get update && apt-get install -y wget openjdk-7-jre openjdk-7-jdk
ENV JAVA_HOME /usr/lib/jvm/jdk
RUN ln -s /usr/lib/jvm/java-7-openjdk-amd64 $JAVA_HOME
RUN wget -q -O - http://apache.mirrors.pair.com/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz | tar -xzf - -C /opt \
    && mv /opt/zookeeper-3.4.6 /opt/zookeeper \
    && cp /opt/zookeeper/conf/zoo_sample.cfg /opt/zookeeper/conf/zoo.cfg \
    && mkdir -p /tmp/zookeeper

WORKDIR /opt/zookeeper

ENTRYPOINT ["/opt/zookeeper/bin/zkServer.sh"]
CMD ["start-foreground"]
