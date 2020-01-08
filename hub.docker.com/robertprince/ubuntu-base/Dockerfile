FROM ubuntu:16.04

MAINTAINER Robert Prince "robert@robertprince.net"

RUN apt-get update && apt-get install -y build-essential \
git \
autoconf \
unzip \
screen \
python \
curl \
vim \
wget

RUN apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
