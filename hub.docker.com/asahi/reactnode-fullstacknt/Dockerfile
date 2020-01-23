FROM golang:1-alpine

RUN set -x \
    && apk add --no-cache git \
    && go get github.com/bitly/oauth2_proxy

EXPOSE 4180

