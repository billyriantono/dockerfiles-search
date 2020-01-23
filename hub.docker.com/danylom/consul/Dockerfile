############################################################
# Dockerfile to build an consul cluster
# Based on Ubuntu
############################################################
FROM ubuntu:latest

MAINTAINER Danylo Mancari (danylo.mancari@gmail.com)

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get install -y curl wget ssh unzip

RUN wget https://releases.hashicorp.com/consul/0.6.0/consul_0.6.0_linux_amd64.zip
RUN unzip consul_0.6.0_linux_amd64.zip -d /usr/local/bin/
RUN rm consul_0.6.0_linux_amd64.zip
RUN mkdir -p /etc/consul.d/bootstrap/
RUN mkdir /etc/consul.d/server/
RUN mkdir /etc/consul.d/client/

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

ENTRYPOINT tail -f /dev/null
