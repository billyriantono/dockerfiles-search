# DOCKER-VERSION	1.4.1

FROM ubuntu:14.04
MAINTAINER Nathaniel Hoag, info@nathanielhoag.com

RUN apt-get update && \
  apt-get install -y wget && \
  wget -q -O - https://deb.nodesource.com/setup_0.12 | sudo bash - && \
  apt-get install -y build-essential nodejs && \
  rm -rf /var/lib/apt/lists/*
