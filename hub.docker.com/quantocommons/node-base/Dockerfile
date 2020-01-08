FROM alpine:3.7

MAINTAINER Lucas Teske <lucas@contaquanto.com.br>

# App Base
RUN apk add --update unzip nodejs gnupg git openssh python python3 make gcc g++ autoconf bash

RUN npm -g install babel-cli babel-register rimraf pm2 yarn babel-plugin-typecheck

WORKDIR /
