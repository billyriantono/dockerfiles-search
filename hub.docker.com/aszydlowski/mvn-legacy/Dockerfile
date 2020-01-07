FROM maven:3-jdk-8-alpine AS builder
LABEL maintainer="Adam Szydłowski <aszydlowski@isolution.pl>"

RUN apk add --no-cache --update \
    nodejs \
    npm \
    git \
    && npm install -g bower \
    && npm install -g bower-art-resolver \
    && npm install -g gulp