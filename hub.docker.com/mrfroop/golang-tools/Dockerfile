FROM golang:1.9.1-alpine3.6

LABEL maintainer="mrfroop <fredrik@jambren.com>"

RUN apk --no-cache add \
	git

RUN go get -u github.com/golang/lint/golint

WORKDIR $GOPATH
