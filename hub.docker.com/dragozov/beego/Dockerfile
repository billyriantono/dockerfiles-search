FROM golang:1.8

MAINTAINER Plamen Dragozov "plamen@dragozov.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get update && apt-get -y install --no-install-recommends gettext adduser

RUN go get bitbucket.org/liamstask/goose/cmd/goose
RUN go get github.com/beego/bee
RUN go get github.com/jstemmer/go-junit-report
RUN go get github.com/smartystreets/goconvey
RUN go get golang.org/x/tools/cmd/cover
