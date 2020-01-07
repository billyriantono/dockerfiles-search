FROM node:alpine
LABEL maintainer="r.owliaei@gmail.com"

RUN apk update && \
  rm -rf /var/cache/apk/*

RUN mkdir -p /usr/src/app &&\
  chown node:node /usr/src/app

ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
ENV PATH=$PATH:/home/node/.npm-global/bin

WORKDIR /usr/src/app
USER node
RUN npm i -g total.js
