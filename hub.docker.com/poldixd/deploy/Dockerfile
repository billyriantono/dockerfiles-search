# https://hub.docker.com/_/alpine/
FROM alpine:3.7

MAINTAINER Nils Poltmann <dev@nils.li>

RUN apk update \
 && apk upgrade \
 && apk add --no-cache \
            bash \
            rsync \
            openssh-client \
            zip \
            unzip \
 && rm -rf /var/cache/apk/*
