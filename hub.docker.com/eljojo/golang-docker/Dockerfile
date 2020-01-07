FROM debian:wheezy

RUN apt-get update && apt-get install --no-install-recommends -y \
    ca-certificates \
    curl \
    mercurial \
    git-core

# update everything because of shellshock
RUN apt-get upgrade -y
RUN apt-get upgrade -y --force-yes bash

RUN curl -s https://storage.googleapis.com/golang/go1.3.2.linux-amd64.tar.gz | tar -v -C /usr/local -xz

ENV GOPATH /go
ENV GOROOT /usr/local/go
ENV PATH $PATH:/usr/local/go/bin:/go/bin
