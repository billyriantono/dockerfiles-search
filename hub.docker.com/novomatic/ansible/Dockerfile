FROM ubuntu:18.10

RUN apt-get update && apt-get install -y software-properties-common \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt-get install -y ansible=2.8.2-1ppa~cosmic vim rsync

WORKDIR /opt/ansible