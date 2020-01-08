FROM node:8-alpine

LABEL maintainer="dc.duong@neopost.com"

RUN apk --no-cache add \
      bash \
      g++ \
      ca-certificates \
      lz4-dev \
      musl-dev \
      cyrus-sasl-dev \
      openssl-dev \
      make \
      python

RUN apk add --no-cache --virtual .build-deps gcc zlib-dev libc-dev bsd-compat-headers py-setuptools bash

# Create app directory
RUN mkdir -p /usr/local/app

COPY package.json /usr/local/app/package.json

# Move to the app directory
WORKDIR /usr/local/app

# Install node-rdkafka
RUN npm install