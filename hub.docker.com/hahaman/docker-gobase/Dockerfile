ARG GO_VERSION=1.13.0

FROM golang:${GO_VERSION}-alpine AS builder

RUN apk update && apk upgrade && apk add --no-cache git \
    && git config --global http.https://gopkg.in.followRedirects true

RUN go get -v github.com/gorilla/mux \
    github.com/spf13/viper \
	github.com/Shopify/sarama

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64