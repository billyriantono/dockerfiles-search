FROM golang:1.9.0-alpine3.6 AS build

RUN apk add --no-cache --virtual git musl-dev
RUN go get github.com/gohugoio/hugo

from alpine:3.6
COPY --from=build /go/bin/hugo /bin/hugo
WORKDIR /site
EXPOSE 1313