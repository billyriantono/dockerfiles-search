FROM golang:1.13-alpine as builder
ENV GO111MODULE on

RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del .build-dependencies

RUN apk add --no-cache \
        git