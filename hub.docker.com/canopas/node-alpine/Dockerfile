FROM node:10.8.0-alpine
MAINTAINER Shweta Patel <patelshwetag@gmail.com>

RUN apk update && apk add bash git && rm -rf /var/cache/apk/*

RUN npm install mocha -g
RUN npm install forever -g
