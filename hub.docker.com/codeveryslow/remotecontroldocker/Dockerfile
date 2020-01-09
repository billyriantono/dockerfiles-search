FROM ubuntu:latest
MAINTAINER codeVerySlow <280998677@qq.com>

#ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && apt-get install -y \
    libgoogle-glog-dev \
    libfcgi-dev \
    libjsoncpp-dev \
    libmemcached-dev \
    libcrypto++-dev \
    libmysqlclient-dev \
    git \
    make \
    g++ \
  && apt-get clean
