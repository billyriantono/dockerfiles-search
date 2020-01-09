FROM golang

MAINTAINER Darren Jones version: 0.1

ADD . /go/src/github.com/dazjones/go-pets
RUN apt-get update && \
    apt-get install unzip && \
    wget https://github.com/dazjones/go-pets/archive/v0.1.zip && \
    unzip v*.zip && \
    cp -r go-pets-*/* /go/src/github.com/dazjones/go-pets
RUN cd /go/src/github.com/dazjones/go-pets && \
    go get
RUN go install github.com/dazjones/go-pets && \
    rm -rf /go/src/* /go/packages/*

ENTRYPOINT /go/bin/go-pets
EXPOSE 8080

