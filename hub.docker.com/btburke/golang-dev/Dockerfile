FROM ubuntu

RUN apt-get update && apt-get -y upgrade && apt-get install -y git wget && wget https://storage.googleapis.com/golang/go1.4.linux-amd64.tar.gz && tar -C /usr/local -xzf go1.4.linux-amd64.tar.gz && rm go1.4.linux-amd64.tar.gz

RUN mkdir -p /golang

ENV GOPATH /golang
ENV PATH /usr/local/go/bin:/golang/bin:$PATH

RUN go get github.com/smartystreets/goconvey

EXPOSE 10001

WORKDIR /golang

ENTRYPOINT ["goconvey", "-port", "10001"]


