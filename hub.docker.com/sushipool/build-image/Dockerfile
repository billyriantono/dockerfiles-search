FROM node:9
MAINTAINER brantje <brantje@gmail.com>

ENV VERSION=v9.11.1 NPM_VERSION=5.8.0

RUN apt update
RUN apt install -y apt-utils ca-certificates wget curl tar python python-dev python-pip util-linux build-essential && \
    npm install -g node-gyp pkg@4.3.1
