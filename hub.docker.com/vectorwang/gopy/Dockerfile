FROM python:3.6-alpine

MAINTAINER Vector Wang
# this docker file for enviornment of Python3.6.8 + Go-devel

RUN set -ex \
    && apk update \
    && apk add --no-cache \
    go \
    git \
    curl \
    gcc \
    g++ \
    openssl-dev \
    openssh

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" "$GOPATH/pkg" \
  && chmod -R 777 "$GOPATH"

WORKDIR /go
RUN go get -u github.com/go-delve/delve/cmd/dlv
#    && go get github.com/DataDog/go-python3 \
#    && go get -u github.com/golang/protobuf/protoc-gen-go \
#    && go get github.com/RichardKnop/machinery/v1 \
#    && echo "golang env complete"
#
#RUN pip install sqlalchemy \
#        requests \
#        beautifulsoup4 \
#        slimit \
#        selenium


