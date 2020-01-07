FROM ubuntu:latest

MAINTAINER Vishnu Prasad <vishnu667@gmail.com>

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="e.g. https://github.com/vishnu667/dockerImages" \
      org.label-schema.vcs-ref=$VCS_REF

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*

WORKDIR /root
