FROM ubuntu:latest
MAINTAINER Andreas Oeldemann <hey@aoel.io>

RUN apt-get update \
 && apt-get install -y vim wget curl inetutils-ping net-tools git \
 && rm -rf /var/lib/apt/lists/*

ENV LANG C.UTF-8
