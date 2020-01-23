FROM ubuntu:18.04
MAINTAINER timiil@163.com
  
RUN apt-get update -y && \
  apt-get upgrade -y && \
  apt-get install -y wget unzip curl && \
  wget https://releases.hashicorp.com/consul-template/0.23.0/consul-template_0.23.0_linux_amd64.zip && \
  unzip consul-template_0.23.0_linux_amd64.zip && \
  mv consul-template /usr/local/bin/
