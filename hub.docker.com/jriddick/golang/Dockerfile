FROM golang:alpine
MAINTAINER jriddick

# Fetch package dependencies
RUN apk update && apk add git \
  make \
  bzr \
  mercurial \
  subversion \
  sqlite-dev \
  curl \
  && rm -rf /var/cache/apk/*

# Fetch golang dependencies
RUN go get -u github.com/Masterminds/glide
RUN go get -u github.com/onsi/ginkgo/ginkgo
RUN go get -u github.com/canthefason/go-watcher/cmd/watcher

# Enable vendoring
ENV GO15VENDOREXPERIMENT 1
