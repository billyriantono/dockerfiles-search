FROM alpine:latest
MAINTAINER Valentin Fries <contact@fries.io>

ENV USER=root

RUN apk add --no-cache g++ make git vim &&\
    rm -rf /var/cache/apk/* &&\
    mkdir /src

WORKDIR /src