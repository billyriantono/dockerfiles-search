FROM ubuntu:bionic
MAINTAINER HermesCK
RUN apt-get update && \
    apt-get install --no-install-recommends -y software-properties-common && \
    apt-add-repository ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible git mc nano wget curl && \
    mkdir /root/bin && mkdir /root/work
    
COPY bin/* /root/bin/

WORKDIR /root/work
