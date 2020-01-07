FROM alpine:latest

LABEL MAINTAINER="Aurélien Satger"

ARG IONIC_VERSION="5.4.9"

RUN apk update \
  && apk add openssh \
  && apk add --update nodejs nodejs-npm \
  && npm i -g ionic@${IONIC_VERSION}

