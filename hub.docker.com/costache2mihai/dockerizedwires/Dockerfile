FROM node:alpine

MAINTAINER Coroin LLC <info@coroin.com>

RUN apk --no-cache add autoconf automake g++ gcc git make \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

ENTRYPOINT ["npm"]