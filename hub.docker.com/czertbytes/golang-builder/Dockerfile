FROM golang:1.6-alpine
MAINTAINER Daniel Hodan <daniel.hodan@czertbytes.de>

RUN apk update
RUN apk add gcc
RUN apk add musl-dev
RUN apk add bash git

RUN mkdir -p /go/src/github.com/appc
RUN git clone https://github.com/appc/acbuild /go/src/github.com/appc/acbuild
WORKDIR /go/src/github.com/appc/acbuild
RUN /go/src/github.com/appc/acbuild/build \
  && cp /go/src/github.com/appc/acbuild/bin/acbuild /go/bin

CMD sh
