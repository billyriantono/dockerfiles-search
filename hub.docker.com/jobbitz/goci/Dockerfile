FROM golang:1.11.0-alpine3.7

RUN apk update  && \
  apk upgrade --update-cache --available  && \
  apk add git make curl perl build-base

RUN wget -O - -q https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

RUN wget -O - -q https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s v1.15.0

WORKDIR $GOPATH
