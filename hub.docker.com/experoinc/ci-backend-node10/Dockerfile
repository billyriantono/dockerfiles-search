FROM node:10-alpine

WORKDIR /usr/src

RUN \
  apk --no-cache add python py-pip build-base gcc wget git && \
  pip install --no-cache-dir awscli
