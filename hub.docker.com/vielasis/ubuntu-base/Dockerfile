FROM ubuntu:16.04

MAINTAINER Viel Asis <its.viel@gmail.com>

# Make sure our locale is en_US and UTF-8
RUN locale-gen en_US.UTF-8

# Install necessary packages
RUN apt-get update -qq \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install curl wget rsync sudo expect \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install git \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install python \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install zip unzip \
  && DEBIAN_FRONTEND=noninteractive apt-get -y install tree \
  && rm -rf /var/lib/apt/lists/*

# Version name
ENV UBUNTU_BASE_REV 1.0.0