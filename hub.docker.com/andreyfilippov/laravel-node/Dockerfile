FROM node:6-alpine

RUN apk --update add python make g++ \
  && rm -rf /var/cache/apk/*

RUN npm install -g npm

WORKDIR /var/www/html
