FROM centos:centos7

MAINTAINER Charles Chen <charlestg@yahoo.com>


ENV GOROOT=/usr/local/go
ENV GOPATH=/opt/go
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin
ENV GOVERSION=1.11.2

RUN yum -y update && yum -y upgrade && \
    yum -y install epel-release && \
    yum -y install wget git sudo bzip2 tmux gcc openssl

WORKDIR /tmp
RUN curl https://storage.googleapis.com/golang/go$GOVERSION.linux-amd64.tar.gz | tar -xz
RUN mkdir -p /opt
RUN mv ./go $GOROOT
RUN go version

RUN mkdir -p $GOPATH

RUN echo 'export PATH=/usr/local/bin:$PATH' >> /etc/profile


