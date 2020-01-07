FROM ubuntu:latest
MAINTAINER Galileo Martinez "playgali@gmail.com"
ENV REFRESHED_AT 2018-Jun-08
ENV ANSIBLE_VERSION 2.3.2.0

RUN apt-get update && apt-get install curl nano vim python-pip -y \
 && pip install ansible==$ANSIBLE_VERSION \
 && rm -rf /var/lib/apt/lists/*
