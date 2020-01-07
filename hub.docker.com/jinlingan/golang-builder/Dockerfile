FROM golang:1.13.5-buster


RUN go get -u github.com/golang/dep/cmd/dep

RUN apt-get update && apt-get install ruby ruby-dev rubygems build-essential rpm lsof -y && apt-get clean

RUN gem install --no-document fpm

RUN curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.21.0

RUN go get -u golang.org/x/tools/...