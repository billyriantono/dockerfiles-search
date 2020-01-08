FROM node:8.12-alpine

ENV DOCKERIZE_VERSION v0.6.1

RUN apk upgrade && \
    apk update && \
    apk add --no-cache xvfb \
    openssl \
    openjdk8-jre-base \
    python \
    gcc \
    g++ \
    musl-dev \
    make

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz
