FROM golang:1.13.5-alpine3.11

RUN apk add --no-cache docker tcl tk expect git wget
RUN apk add --update -t build-deps libc-dev gcc libgcc

RUN go get -u golang.org/x/lint/golint

RUN wget -O - -q https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh -s v1.22.2
RUN golangci-lint --version
