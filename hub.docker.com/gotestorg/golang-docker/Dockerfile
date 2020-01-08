FROM ubuntu:14.04.1
MAINTAINER Sebastian Müller <info@sebastian-mueller.net>
RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl build-essential ca-certificates git mercurial bzr

RUN mkdir /goroot
RUN mkdir -p /gopath/src

# SHA1 checksum from http://golang.org/dl
RUN echo '3e871200e13c0b059b14866d428910de0a4c51ed go1.4.1.linux-amd64.tar.gz' > go1.4.1.linux-amd64.tar.gz.sha1
RUN curl -O -s https://storage.googleapis.com/golang/go1.4.1.linux-amd64.tar.gz
RUN sha1sum —check go1.4.1.linux-amd64.tar.gz.sha1
RUN tar xvzf go1.4.1.linux-amd64.tar.gz -C /goroot --strip-components=1

ENV GOROOT /goroot
ENV GOPATH /gopath
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin
