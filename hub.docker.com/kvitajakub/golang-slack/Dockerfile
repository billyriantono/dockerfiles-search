FROM golang:1.12.6-alpine
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
RUN go get github.com/nlopes/slack
