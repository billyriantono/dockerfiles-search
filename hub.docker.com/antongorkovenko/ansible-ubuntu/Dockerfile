FROM ubuntu:18.04

RUN \
  apt-get update && \
  apt-get install -y software-properties-common && \
  apt-add-repository ppa:ansible/ansible && \
  apt-get update && \
  apt-get install -y ansible && \
  rm -rf /var/lib/apt/lists/* && apt-get clean all
 
RUN mkdir /ansible
WORKDIR /ansible
