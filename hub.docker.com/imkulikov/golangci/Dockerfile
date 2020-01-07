FROM golang:1.10.3-alpine3.7

# Prepare environment
RUN apk add --no-cache git bash make ca-certificates curl gcc musl-dev

# Install dep
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

# Install golangci-lint
RUN curl -sfL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | sh