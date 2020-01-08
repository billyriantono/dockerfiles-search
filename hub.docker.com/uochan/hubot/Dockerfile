FROM node:0.10
MAINTAINER uochan

RUN apt-get update && \
    apt-get install -y redis-server
RUN npm install -g yo generator-hubot

RUN apt-get clean &&\
    rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
