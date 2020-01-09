FROM ubuntu:18.04

WORKDIR /ansible

RUN apt-get update \
    && apt upgrade -y \
    && apt install software-properties-common -y \
    && apt-add-repository --yes --update ppa:ansible/ansible \
    && apt install ansible -y

EXPOSE 22