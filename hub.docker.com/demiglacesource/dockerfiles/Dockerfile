FROM centos:centos7
MAINTAINER demiglacesource <demiglacesource@gmail.com>

RUN yum update -y
RUN yum install -y \
  wget \
  unzip \
  telnet \
  tcpdump \
  java-1.7.0-openjdk.x86_64 

RUN cd /opt && wget http://download.forgerock.org/downloads/openidm/snapshot/openidm-3.2.0-SNAPSHOT.zip
RUN unzip /opt/openidm-3.2.0-SNAPSHOT.zip -d /opt
RUN sh /opt/openidm/bin/create-openidm-rc.sh
RUN cp /opt/openidm/bin/openidm /etc/init.d/

VOLUME [ '/opt/openidm/conf', '/opt/openidm/logs', '/opt/openidm/script' ]

EXPOSE 8443
EXPOSE 8080

ENTRYPOINT ./opt/openidm/startup.sh

