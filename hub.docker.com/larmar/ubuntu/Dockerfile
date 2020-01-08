FROM ubuntu:14.04.1
MAINTAINER martin.wilderoth@gmail.com

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
 && apt-get update \
 && apt-get install -y wget \
 && rm -rf /var/lib/apt/lists/* 

