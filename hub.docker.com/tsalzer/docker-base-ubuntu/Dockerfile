FROM ubuntu:18.04

MAINTAINER Till Salzer <till.salzer@gmail.com>

ENV base_ubuntu_version 18.04

LABEL description="Base Ubuntu image" \
      net.tsalzer.docker-base-ubuntu.version="${base_ubuntu_version}"

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget

