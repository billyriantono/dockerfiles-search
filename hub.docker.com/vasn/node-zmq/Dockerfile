# Set node base image
FROM node:6

# File Author / Maintainer
MAINTAINER Vas N <phpvas@gmail.com>

#Install ZeroMQ
ENV ZMQ_VERSION 4.1.4
RUN wget https://github.com/zeromq/zeromq4-1/releases/download/v$ZMQ_VERSION/zeromq-$ZMQ_VERSION.tar.gz -P /tmp && \
    tar -zxvf /tmp/zeromq-$ZMQ_VERSION.tar.gz -C /tmp && cd /tmp/zeromq-$ZMQ_VERSION && ./autogen.sh && \
    ./configure --without-libsodium && make && make install && ldconfig

# Clean up
RUN rm -rf /tmp/*
