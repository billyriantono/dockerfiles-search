# Dockerfile for Node.js

FROM phusion/baseimage
MAINTAINER Sebastien Pujadas http://pujadas.net
ENV REFRESHED_AT 2015-05-08

### install Node.js

RUN apt-get update -qq \
 && apt-get install -qqy curl git \
 && curl -sL https://deb.nodesource.com/setup_0.12 | bash - \
 && apt-get install -qqy nodejs \
 && apt-get clean
