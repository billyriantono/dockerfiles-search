FROM debian:jessie

MAINTAINER Travix

# install dependencies
RUN apt-get update \
    && apt-get install -y \
        curl \
        unzip \
        make \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
