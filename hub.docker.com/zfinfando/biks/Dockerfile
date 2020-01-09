FROM golang:buster as confd
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install unzip make

ARG CONFD_VERSION=0.16.0
ADD https://github.com/kelseyhightower/confd/archive/v${CONFD_VERSION}.tar.gz /tmp/

RUN mkdir -p /go/src/github.com/kelseyhightower/confd && \
  cd /go/src/github.com/kelseyhightower/confd && \
  tar --strip-components=1 -zxf /tmp/v${CONFD_VERSION}.tar.gz && \
  go install github.com/kelseyhightower/confd && \
  rm -rf /tmp/v${CONFD_VERSION}.tar.gz

FROM tomcat:slim

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install git

ADD https://zfinfando:Finfando67@api.bitbucket.org/2.0/repositories/zfinfando/biks-install/commit/master /info
RUN git clone https://zfinfando:Finfando67@bitbucket.org/zfinfando/biks-install.git /opt/biks

VOLUME /opt/biks/data
VOLUME /usr/local/tomcat/conf/Catalina/localhost

COPY --from=confd /go/bin/confd /usr/local/bin/confd
COPY biks-docker-init.sh /opt/biks/

RUN mkdir -p /etc/confd/conf.d && \
  mkdir -p /etc/confd/templates && \
  chmod 777 /opt/biks/*.sh

COPY *.toml /etc/confd/conf.d/
COPY *.tmpl /etc/confd/templates/
COPY BIKS.xml /usr/local/tomcat/conf/Catalina/localhost/

ENV foxyConfigsDir /opt/biks/cfg
ENV BIKS_VER 1.8.5.18
ENV BIKS_SQLSRV mssql
ENV BIKS_SQLINST ""
ENV BIKS_DB biks-docker
ENV BIKS_SA sa
ENV BIKS_PWD Bssg4ever

ENV CATALINA_OPTS "-Xms512m -Xmx2048m -XX:PermSize=64m -XX:MaxPermSize=128m"

CMD ["sh","-c","cd /opt/biks && ./biks-docker-init.sh && catalina.sh run"]
