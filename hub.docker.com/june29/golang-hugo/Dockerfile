FROM golang:latest

RUN set -x && \
    go get -d github.com/gohugoio/hugo && \
    go get -d github.com/wellington/go-libsass && \
    cd ${GOPATH:-$HOME/go}/src/github.com/gohugoio/hugo && \
    go install --tags extended
