FROM centos:7

MAINTAINER Andrew Kursar <drew@kursar.org>

## Oracle JDK8
RUN curl -L -o /tmp/java.rpm \
  --cookie oraclelicense=accept-securebackup-cookie \
  http://download.oracle.com/otn-pub/java/jdk/8u51-b16/jdk-8u51-linux-x64.rpm && \
  yum install -y /tmp/java.rpm && \
  yum clean all && \
  rm -fr /tmp/*

## Install Teamcity
RUN curl -L -o /tmp/teamcity.tgz \
  http://download.jetbrains.com/teamcity/TeamCity-9.1.1.tar.gz && \
  tar zxf /tmp/teamcity.tgz -C /opt && \
  rm -fr /tmp/*

EXPOSE 8111

VOLUME ["/teamcity"]

ENV TEAMCITY_DATA_PATH /teamcity

CMD ["/opt/TeamCity/bin/teamcity-server.sh", "run"]
