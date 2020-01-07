FROM golang:1.13
MAINTAINER Toshiaki Baba<toshiaki@netmark.jp>

RUN go get -u golang.org/x/vgo
RUN go get -u github.com/golang/dep/cmd/dep
ENV GO111MODULE on
RUN go get -u golang.org/x/tools/cmd/goimports
RUN go get -u golang.org/x/lint/golint
RUN go get -u github.com/mitchellh/gox
RUN go get -u github.com/Songmu/goxz/cmd/goxz
RUN go get -u github.com/haya14busa/goverage
RUN go get -u github.com/go-delve/delve/cmd/dlv
