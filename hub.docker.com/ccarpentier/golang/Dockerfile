FROM ubuntu:trusty
MAINTAINER Chris Carpentier "coredump@gmail.com"

RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates curl wget && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends bzr git mercurial openssh-client subversion && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends g++ gcc libc6-dev make && rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION=1.5.1
ENV GOLANG_VERSION=1.5.1
ENV GOLANG_DOWNLOAD_URL=https://golang.org/dl/go1.5.1.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA1=46eecd290d8803887dec718c691cc243f2175fe0

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz && echo "$GOLANG_DOWNLOAD_SHA1 golang.tar.gz" | sha1sum -c - && tar -C /usr/local -xzf golang.tar.gz && rm golang.tar.gz

ENV GOPATH=/go
ENV PATH=/go/bin:/usr/local/go/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
