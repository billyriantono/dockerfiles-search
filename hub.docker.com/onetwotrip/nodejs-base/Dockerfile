FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN \
 apt-get update && \
 apt-get install -y build-essential curl git python-minimal && \
 curl -sL https://deb.nodesource.com/setup_0.10 | sudo -E bash - && \
 sudo apt-get install -y nodejs libexpat1 libexpat1-dev libuuid1 libmysqlclient-dev libzmq3-dev && \
 rm -rf /var/lib/apt/lists/*
