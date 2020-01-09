FROM ubuntu:xenial
MAINTAINER Stefan Kaestle <stefan.kaestle@inf.ethz.ch>

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
        libnuma-dev \
        git \
    && apt-get clean && rm -rf /var/lib/apt/lists/*
