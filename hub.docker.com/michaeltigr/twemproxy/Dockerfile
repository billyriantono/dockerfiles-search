FROM ubuntu:16.04

LABEL maintainer "Michael Molchanov <mmolchanov@adyax.com>"

RUN apt-get update \
  && apt-get -y install \
  bash \
  build-essential \
  curl \
  openssl \
  software-properties-common \
  wget \
  && add-apt-repository ppa:twemproxy/stable \
  && apt-get update \
  && apt-get -y install twemproxy \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/sbin/nutcracker"]
