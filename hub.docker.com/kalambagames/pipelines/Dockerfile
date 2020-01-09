FROM mhart/alpine-node:8.15.1
LABEL version="2.1.0"
LABEL maintainer="Michal Ochman <michal@kalambagames.com>"

ENV NODE_PATH=/usr/lib/node_modules

RUN \
  apk update &&\
  # install build dependencies
  apk add --no-cache --virtual runtime-dependencies \
    cairo \
    giflib \
    git \
    jpeg \
    pixman \
    pango &&\
  apk add --no-cache --virtual build-dependencies \
    g++ \
    make \
    python &&\
  apk add --no-cache --virtual canvas-build-dependencies \
    build-base \
    cairo-dev \
    freetype-dev \
    giflib-dev \
    jpeg-dev \
    libjpeg-turbo-dev \
    pango-dev \
    pangomm-dev \
    pixman-dev &&\
  # allows npm to install globally (-g)
  npm config set user 0 &&\
  npm config set unsafe-perm true &&\
  # install canvas for jsdom
  npm install -g canvas@2.3.1 --build-from-source &&\
  # delete build dependencies
  apk del build-dependencies &&\
  apk del canvas-build-dependencies &&\
  rm /var/cache/apk/*
