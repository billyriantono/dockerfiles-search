FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

RUN \
  apt-get update && \
  apt-get install -y libguestfs-tools && \
  apt-get install -y linux-image-virtual && \
  rm -rf /var/lib/apt/lists/*
