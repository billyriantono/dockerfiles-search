FROM ubuntu:15.04

MAINTAINER kaizyu <enzo@coverit.io>

RUN apt-get update

# Install wget
RUN apt-get install -y wget

# Install git
RUN apt-get install -y git

# Install pkg-config
RUN apt-get install -y pkg-config

# Install libgit2-22
RUN apt-get install -y libgit2-dev

# Install golang
RUN wget -q https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.4.2.linux-amd64.tar.gz && \
    rm go1.4.2.linux-amd64.tar.gz
ENV GOPATH /go
ENV PATH $PATH:/usr/local/go/bin:$GOPATH/bin
