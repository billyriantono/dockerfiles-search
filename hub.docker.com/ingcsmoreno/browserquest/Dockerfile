FROM node:7.9.0-alpine

MAINTAINER Carlos S. Moreno <ingcsmoreno@gmail.com>

ENV SERVER_PORT 8000
ENV NB_PLAYERS 200
ENV NB_WORLDS 5
ENV REDIS_HOST redis
ENV REDIS_PORT 6379
ENV DOCKERIZE_VERSION v0.4.0

RUN apk add --update git python g++ make wget tar  \
  && git clone git://github.com/browserquest/BrowserQuest.git gamequest \
  && cd gamequest \
  && npm config set registry http://registry.npmjs.org/ \
  && npm install -d \
  && wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
  && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
  && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
  && apk del git g++ make wget tar \
  && rm -rf /var/cache/apk/*

COPY config/* /gamequest/server/

WORKDIR gamequest

EXPOSE 8000

CMD dockerize -template /gamequest/server/config.tmpl:/gamequest/server/config.json node server/js/main.js