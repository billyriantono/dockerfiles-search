FROM golang:1.10.3

RUN go get -u github.com/golang/vgo

RUN go get -u github.com/golangci/golangci-lint/cmd/golangci-lint

#RUN go get -u github.com/alecthomas/gometalinter

#RUN gometalinter --install

ENV CC=gcc

WORKDIR /go_app
