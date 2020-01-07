FROM node:10-alpine

RUN apk add --no-cache make gcc g++ python git rsync openssh autoconf automake \
    && rm -rf /var/lib/apt/lists/* \
    /var/cache/apk/* \
    /usr/share/man \
    /tmp/* 

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
