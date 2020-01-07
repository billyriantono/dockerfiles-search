FROM golang:1.12-alpine

ENV GIN_MODE=release

RUN apk --no-cache --update add gcc g++ make bash git curl

RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
