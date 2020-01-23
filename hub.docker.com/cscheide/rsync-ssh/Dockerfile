# https://hub.docker.com/_/alpine/
FROM alpine:latest

RUN apk update \
 && apk upgrade \
 && apk add --no-cache \
            rsync \
            openssh-client \
 && rm -rf /var/cache/apk/*
