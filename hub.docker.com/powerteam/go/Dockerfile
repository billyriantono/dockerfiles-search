FROM ubuntu:10.04

# APT requirements:
RUN apt-get update -y
RUN apt-get install -y -q curl build-essential ca-certificates
RUN rm -rf /var/lib/apt/lists/*

# Golang install:
ENV GOVERSION 1.4.2
ENV GOROOT /goroot
RUN mkdir $GOROOT && curl https://storage.googleapis.com/golang/go${GOVERSION}.linux-amd64.tar.gz | tar xvzf - -C $GOROOT --strip-components=1
ENV PATH $PATH:$GOROOT/bin

# Working dir:
ENV GOPATH /code
RUN mkdir -p /code
VOLUME /code
WORKDIR /code
