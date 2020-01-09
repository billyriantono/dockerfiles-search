FROM node:10.16.0-alpine

ARG ENVIRONMENT=development
ENV NODE_ENV=${ENVIRONMENT}

WORKDIR /usr/src/app

# Install docker
RUN apk add --update docker openrc
RUN rc-update add docker boot

RUN npm install -g yarn

# Needed for libsodium build
RUN apk add build-base python libtool autoconf automake
RUN npm install -g node-gyp