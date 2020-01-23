FROM golang:1.10-alpine

RUN apk add --no-cache git \
    && go get github.com/prometheus/prometheus/cmd/promtool \
    && apk del git

ENTRYPOINT [ "promtool", "check", "metrics" ]