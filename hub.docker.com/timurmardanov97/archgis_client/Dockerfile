FROM node:alpine

MAINTAINER Mardanov Timur <timurmardanov97@gmail.com>
LABEL ru.archgis.client.version="0.0.3-beta"
LABEL ru.archgis.client.vendor="Archgis Institute"
LABEL ru.archgis.client.version="2018-06-02"

WORKDIR '/project'
COPY package.json yarn.lock ./

RUN apk add --no-cache --virtual builder \
 git python make g++ \
 && yarn install --frozen-lockfile

COPY . .

EXPOSE 3000
CMD ["yarn", "start"]
