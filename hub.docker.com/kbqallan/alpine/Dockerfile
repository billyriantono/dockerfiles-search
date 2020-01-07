FROM alpine:3.8
MAINTAINER from allan

ENV TERM=linux
RUN set -x && apk upgrade --update --no-cache && apk add --update --no-cache bash curl ca-certificates openssl curl tar iproute2 supervisor && rm -rf /var/cache/apk/*
