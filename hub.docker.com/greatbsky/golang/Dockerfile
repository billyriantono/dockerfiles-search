FROM greatbsky/centos7:latest
MAINTAINER architect.bian
LABEL name="golang" license="MIT" build-date="20180203"

ENV VERSION 1.9.3
ENV GOROOT /data/env/go
ENV GOPATH /data/env/go/repository
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

RUN yum update -y && cd /data/softs && wget https://dl.google.com/go/go$VERSION.linux-amd64.tar.gz && tar -zvxf go$VERSION.linux-amd64.tar.gz && mv go /data/env/go &&  rm -rf /data/softs/*

CMD ["go", "version"]