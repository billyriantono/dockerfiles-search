FROM golang:1.10
MAINTAINER Antti Kupila <akupila@gmail.com>
ARG DEP_VERSION=0.4.1
ARG GOLANGCI_LINT_VERSION=1.6.1
RUN \
  curl -sL https://github.com/golang/dep/releases/download/v$DEP_VERSION/dep-linux-amd64 -o $GOPATH/bin/dep && \
  chmod +x $GOPATH/bin/dep && \
  curl -sL https://install.goreleaser.com/github.com/golangci/golangci-lint.sh | bash -s v$GOLANGCI_LINT_VERSION && \
  apt-get update && \
  apt-get install -y netcat && \
  apt-get clean
