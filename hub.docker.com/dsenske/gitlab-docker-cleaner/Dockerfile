# build stage
FROM golang:1.12-alpine3.9 AS build-env

ARG GODEP_VERSION=0.5.1

RUN apk add --no-cache git \
    && wget https://github.com/golang/dep/releases/download/v${GODEP_VERSION}/dep-linux-amd64 -O /usr/local/bin/dep \
    && chmod +x /usr/local/bin/dep \
    && go get github.com/mitchellh/gox

WORKDIR /go/src/app
COPY . .

RUN dep ensure \
    && gox -os=linux -arch=amd64 -output=application -ldflags "-X main.applicationVersion=`git rev-parse --short HEAD`" .

# application stage
FROM alpine:3.9
RUN apk add --no-cache ca-certificates

WORKDIR /opt
COPY --from=build-env /go/src/app/application .
CMD ["./application"]