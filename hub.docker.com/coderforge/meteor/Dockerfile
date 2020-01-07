FROM node

MAINTAINER Daithi Coombes <webeire@gmail.com>

RUN apt-get update && \
  apt-get -y upgrade

RUN curl https://install.meteor.com/ | sh

ENV LC_ALL=en_GB.UTF-8
RUN mkdir /app
WORKDIR /app

RUN cd /app && \
  meteor create coder-forge

###
#
# 1. Volume of a default app
# 2. Run meteor as cmd
