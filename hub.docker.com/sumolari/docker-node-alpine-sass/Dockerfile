FROM node:10-alpine

RUN \
  apk update && \
  apk upgrade && \
  apk add --no-cache --virtual build-dependencies make gcc g++ python && \
  yarn global add node-sass && \
  rm -rf /var/cache/apk/*
