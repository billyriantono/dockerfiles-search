# base-ubuntu
FROM lsiobase/ubuntu:bionic

ARG DEBIAN_FRONTEND="noninteractive"

RUN \
  echo "** Checkout linuxserver.io whom I have shamelessly **" && \
  echo "** Mimicked thier style and used their baseimages in my Dockers **" && \
  apt-get update && \
  apt-get install -y apt-transport-https && \
  echo "** Installing Packages **" && \
  apt-get install -qy --no-install-recommends \
    ca-certificates \
    software-properties-common \
    wget \
    dkms \
    apt-transport-https \
    git \
    linux-headers-generic \
    build-essential \
    make \
    nano \
    p7zip \
    tar \
    unrar \
    unzip \
    python \
    python3 \
    python-pip \
    python3-pip \
    jq \
    gcc \
    rsync \
    dnsutils && \
  pip install -U setuptools &&\
  echo "** Cleanup **" && \
  apt-get clean && \
  rm -rf \ 
    /root/.cache \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*
