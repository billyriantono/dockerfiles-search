ARG FromImage="golang:1.12-alpine"
FROM ${FromImage} AS build
MAINTAINER tai-ga <masahiro.o@gmail.com>

ENV GOPATH=/go \
	PATH=/go/bin:/usr/local/go/bin:$PATH

RUN apk update \
 && apk upgrade \
 && apk add --no-cache \
        git \
 && go get -u github.com/golang/dep/cmd/dep \
 && go get -u golang.org/x/lint/golint \
 && go get -u github.com/client9/misspell/cmd/misspell \
 && go get -u github.com/gordonklaus/ineffassign \
 && go get -u github.com/fzipp/gocyclo \
 && go get -u github.com/gohugoio/hugo

FROM ${FromImage}
RUN apk update \
  && apk upgrade \
  && apk add --no-cache \
    git \
  && rm -rf /var/cache/apk/*
COPY --from=build /go/bin /go/bin
