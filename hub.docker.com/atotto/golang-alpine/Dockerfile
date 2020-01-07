FROM golang:alpine

RUN apk --no-cache add git

ONBUILD ADD . /go/src/app
ONBUILD RUN go get app

ENTRYPOINT /go/bin/app
