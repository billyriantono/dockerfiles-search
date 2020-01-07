FROM codejuggle/base:latest

RUN apt-get update; apt-get -y upgrade
RUN apt-get -y install bzr gcc git mercurial

ENV GOLANG_VERSION 1.7.4
RUN curl -sSL https://storage.googleapis.com/golang/go$GOLANG_VERSION.linux-amd64.tar.gz | tar -v -C /usr/src -xz

RUN mkdir -p /go/src
ENV GOPATH /go
ENV GOROOT /usr/src/go
ENV PATH /usr/src/go/bin:/go/bin:$PATH
WORKDIR /go
