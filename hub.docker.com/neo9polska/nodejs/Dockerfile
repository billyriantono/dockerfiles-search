#base nodejs neo9 image
FROM ubuntu:trusty

#maintainer info
MAINTAINER Neo9 Polska <contact@neo9.pl>

#to invalidate cache if needed
ENV LAST_UPDATE=2015-04-01

ENV DEBIAN_FRONTEND noninteractive

ENV NODEVERSION v0.12.2

RUN \
    apt-get update && \
    apt-get install -y python python-dev python-pip python-virtualenv wget && \
    rm -rf /var/lib/apt/lists/*
  

RUN \
    cd /tmp/ && \
    wget http://nodejs.org/dist/v0.12.2/node-$NODEVERSION.tar.gz && \
    tar -xvf node-$NODEVERSION.tar.gz && \
    rm -f node-$NODEVERSION.tar.gz && \
    cd node-$NODEVERSION && \
    ./configure && \
    make && \
    make install && \
    rm -rf /tmp/node-$NODEVERSION
    
CMD ["node", "--version"]