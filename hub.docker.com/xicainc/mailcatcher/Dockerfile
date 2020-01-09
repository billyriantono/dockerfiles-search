FROM ruby:alpine

MAINTAINER Xica Inc.

RUN apk add --no-cache g++ musl-dev make sqlite-dev && gem install --no-ri --no-rdoc mailcatcher

EXPOSE 1080 1025

ENTRYPOINT ["mailcatcher", "--smtp-ip=0.0.0.0","--http-ip=0.0.0.0","--foreground"]
