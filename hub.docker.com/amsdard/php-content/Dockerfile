FROM golang:1.13-alpine

RUN set -ex \
    && apk add --no-cache git gcc musl-dev \
    && go get gotest.tools/gotestsum \
    && go get github.com/google/wire/cmd/wire \
    && go get github.com/derekparker/delve/cmd/dlv
