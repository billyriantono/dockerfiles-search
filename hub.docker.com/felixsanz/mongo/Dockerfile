FROM alpine:latest

MAINTAINER Félix Sanz <me@felixsanz.com>

RUN echo http://dl-4.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \
  apk add --update --no-cache mongodb

RUN mkdir -p /data/db

VOLUME /data/db

WORKDIR /data/db

EXPOSE 27017

CMD ["mongod"]
