FROM ubuntu:18.04
MAINTAINER Sincera xdzhang@alauda.io

RUN apt-get update -y
RUN apt-get install sudo -y && \
    apt-get install curl -y && \
    apt-get install supervisor -y && \
    apt-get install python-pip -y && \
    curl -L https://toolbelt.treasuredata.com/sh/install-ubuntu-xenial-td-agent3.sh | sh && rm -rf /var/lib/apt/lists/*
RUN /usr/sbin/td-agent-gem install docker-api

RUN td-agent-gem install fluent-plugin-rewrite-tag-filter

RUN td-agent-gem install fluent-plugin-elasticsearch --no-document
