FROM node:8.1.0-alpine

MAINTAINER Shoma Nishitateno <shoma416@gmail.com>

RUN set -xe \
    && npm install --global webpack@2.5.1

ENV HOME=/home/node

WORKDIR $HOME/app

COPY package.json package-lock.json ./

RUN chown -R node:node $HOME/*

USER node

RUN set -xe \
    && npm install \
    && npm cache clean --force

USER root

COPY . .

RUN set -xe \
    && chown node:node * \
    && chown node:node .* \
    && chown -R node:node build/* \
    && chown -R node:node config/* \
    && chown -R node:node src/* \
    && chown -R node:node test/* 

USER node

RUN npm run build


