FROM ubuntu:14.04.5
MAINTAINER liboni.giovanni@gmail.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
  build-essential \
  cmake \
  unzip \
  wget \
  zip \
  gcc \
  git \
  g++

RUN rm -rf /var/lib/apt/lists/*
RUN apt-get autoclean
RUN apt-get clean
RUN apt-get autoremove
