# Source: https://github.com/rebuy-de/golang-template

FROM golang:1.13-alpine as builder

RUN apk add --no-cache git make curl openssl

# Configure Go
ENV GOPATH=/go PATH=/go/bin:$PATH CGO_ENABLED=0 GO111MODULE=on
RUN mkdir -p ${GOPATH}/src ${GOPATH}/bin

# Install Go Tools
RUN GO111MODULE= go get -u golang.org/x/lint/golint

COPY . /src
WORKDIR /src
RUN set -x \
 && make test \
 && make build \
 && cp /src/dist/prometheus-teamspeak /usr/local/bin/

RUN set -x \
 && prometheus-teamspeak version

FROM alpine:latest

RUN apk add --no-cache ca-certificates
COPY --from=builder /usr/local/bin/* /usr/local/bin/
