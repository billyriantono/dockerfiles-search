FROM ubuntu:18.04

LABEL maintainer="Sagar Patke <https://github.com/sagarpatkeatl>"
LABEL organization="StackRoute <http://stackroute.in>,<https://github.com/stackroute-io>"
LABEL url="https://github.com/stackroute-io"

RUN apt update && apt install -y gnupg && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7BB9C367 && \
    echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu bionic main" | tee - /etc/apt/sources.list.d/ansible.list && \
    apt update && \
    apt install -y git ansible && \
    rm -rf /var/lib/apt/lists/*
