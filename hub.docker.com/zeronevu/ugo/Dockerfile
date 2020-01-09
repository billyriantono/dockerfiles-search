FROM ubuntu:18.04
MAINTAINER ZeroneVu <zeronevu@gmail.com>

# gcc for cgo, and all other common packages
RUN apt-get update && apt-get install -y --no-install-recommends \
  curl \
  ca-certificates \
  build-essential \
  git \
  mercurial \
  bzr \
  && rm -rf /var/lib/apt/lists/*

# Starting environment config, download the go source file
ENV GOLANG_VERSION 1.11.1
ENV GOLANG_DOWNLOAD_URL https://dl.google.com/go/go$GOLANG_VERSION.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 2871270d8ff0c8c69f161aaae42f9f28739855ff5c5204752a8d92a1c9f63993

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

# setting EVN GOPATH, GOBIN
ENV GOPATH /Go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH
ENV GOBIN $GOPATH/bin

COPY go-wrapper /usr/local/bin/

# setting WORKDIR
WORKDIR $GOPATH
