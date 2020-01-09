FROM ubuntu
MAINTAINER Alex SHD 'alex@shdlabs.com'

RUN apt update -y; apt upgrade -y
RUN mkdir /etc/consul.d/ /opt/consul
ADD ./consul /usr/local/bin/
ADD ./consul.conf /etc/

USER root
EXPOSE 8300-8302 8400 8500 8600
CMD consul agent -config-file /etc/consul.conf -ui
