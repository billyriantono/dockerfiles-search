FROM ubuntu:xenial
LABEL maintainer="nickistre@gmail.com"

RUN apt-get update && \
    apt-get install -y software-properties-common openssh-client git && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update && \
    apt-get install -y ansible && \
    rm -rf /var/lib/apt/lists/*

