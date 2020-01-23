FROM java:8-jdk

MAINTAINER Aaron Zirbes <aaron@zirbes.org>

ENV ZK_HOSTS=zookeeper.service.consul:2181 \
     KM_BINTRAY_REPO=aaronzirbes/maven \
     KM_VERSION=1.2.4

ADD https://bintray.com/artifact/download/${KM_BINTRAY_REPO}/kafka-manager-${KM_VERSION}.zip /tmp/kafka-manager.zip
RUN mkdir -p /usr/local
RUN unzip -d /usr/local /tmp/kafka-manager.zip

WORKDIR /usr/local/kafka-manager-${KM_VERSION}

EXPOSE 9000
ENTRYPOINT ["./bin/kafka-manager","-Dconfig.file=conf/application.conf"]
