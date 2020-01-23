FROM ubuntu:wily
MAINTAINER Justin Rupp <jrupp@globalgiving.org>

ENV DEBIAN_FRONTEND noninteractive
RUN \
  apt-get -qq update && \
  apt-get -qqy --force-yes install \
    libboost-all-dev \
    g++ \
    vim \
    git \
    curl \
    libssl-dev \
    libmysqlclient-dev \
  CMake && \
  rm -rf /var/lib/apt/lists/*
RUN \
  cd /tmp && \
  curl -O https://bootstrap.pypa.io/get-pip.py && \
  python get-pip.py && \
  pip install awscli && \
  rm -f get-pip.py

ENTRYPOINT /bin/bash
