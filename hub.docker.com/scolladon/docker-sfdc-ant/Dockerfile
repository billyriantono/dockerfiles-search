FROM alpine

MAINTAINER Sebastien Colladon <colladonsebastien@gmail.com>

RUN apk update
RUN apk add bash
RUN apk add openjdk8
RUN apk add apache-ant --update-cache \
  --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
  --allow-untrusted
RUN apk add --update curl
RUN rm -rf /var/cache/apk/*

ENV ANT_HOME /usr/share/java/apache-ant

ENV PATH $PATH:$ANT_HOME/bin