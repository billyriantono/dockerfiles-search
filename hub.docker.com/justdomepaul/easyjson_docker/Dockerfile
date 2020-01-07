FROM golang:1.11-alpine3.8
RUN apk add --no-cache curl bash git gcc libc-dev build-base

MAINTAINER Max Focker <max.focker.shih@gmail.com>
ENV GO111MODULE=off
RUN go get -u github.com/mailru/easyjson/...
ENTRYPOINT ["easyjson"]