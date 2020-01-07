FROM rawmind/alpine-base:3.8-0
MAINTAINER Raul Sanchez <rawmind@gmail.com>

# Compile and install monit and confd
ENV GOMAXPROCS=2 \
    GOROOT=/usr/lib/go \
    GOPATH=/opt/src \
    GOBIN=/gopath/bin 
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin

# Install and configure golang
RUN mkdir /opt/src && apk add --update git mercurial bzr make go && rm -rf /var/cacke/apk/*

WORKDIR /opt/src

ENTRYPOINT ["bash","-c"]
