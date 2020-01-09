FROM node:alpine

RUN apk add dos2unix bash git --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/community/ --allow-untrusted

WORKDIR /tmp

COPY package.json /tmp/package.json

RUN npm install
