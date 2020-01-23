FROM golang:1.8-alpine

RUN apk add --update git

RUN go get github.com/asciimoo/wuzz

ENTRYPOINT wuzz
