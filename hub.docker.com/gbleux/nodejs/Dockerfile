# VERSION         0.1.0
# DOCKER-VERSION  1.2.0

FROM alpinelinux/base:latest

ENV NPM_CONFIG_GLOBALCONFIG /etc/npmrc
COPY npmrc /etc/npmrc

RUN apk add \
      --virtual docker-nodejs \
      --no-progress \
      --force \
      nodejs && \
    npm -g install npm && \
    npm cache clean