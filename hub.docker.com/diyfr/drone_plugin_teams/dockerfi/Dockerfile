FROM golang:1.11-alpine

WORKDIR /workdir
RUN set -ex \
    && apk add --no-cache git gcc musl-dev \
    && go get -u gotest.tools/gotestsum
