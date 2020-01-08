FROM ubuntu:16.04

RUN apt clean -y

RUN apt update && \
    apt install -y ansible && \
    mkdir -p /root/.ssh

VOLUME ["/etc/ansible", "/root/.ssh"]
WORKDIR /etc/ansible
