FROM maven:3-jdk-7-alpine

MAINTAINER Timoteo Ponce <timo.slack@gmail.com>

RUN apk add --update --no-progress nodejs nodejs-npm unrar bash git mercurial && \ 
  npm install -g bower gulp && \
  rm /var/cache/apk/*
