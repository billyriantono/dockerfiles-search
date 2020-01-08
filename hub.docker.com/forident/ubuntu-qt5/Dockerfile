FROM ubuntu:zesty
MAINTAINER asmaloney@gmail.com

RUN apt-get update && \
    apt-get install -y make g++ make qt5-qmake qt5-default openssh-client && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
