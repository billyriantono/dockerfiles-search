FROM ubuntu:latest

MAINTAINER Claudio Gandelli <claudio.gandelli@looptribe.com>

RUN apt-get update && apt-get install -y \
    rsync \
    lftp

RUN mkdir /data

VOLUME /data
WORKDIR /data