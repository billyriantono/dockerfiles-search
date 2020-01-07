FROM alpine:3.7

ENV GOROOT=/usr/lib/go
ENV GOPATH=/gopath
ENV GOBIN=/gopath/bin
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin

RUN mkdir /data
RUN mkdir /data/inputs
RUN mkdir /data/results
VOLUME [ "/data/results", "/data/inputs" ]

WORKDIR /gopath/src/gobuster
ADD . /gopath/src/gobuster
ADD ./data/wordlists /data/wordlists/

RUN apk add -U git go libc-dev && \
  go get -v gobuster && \
  apk del git go && \
  rm -rf /gopath/pkg && \
  rm -rf /gopath/src && \
  rm -rf /var/cache/apk/*

ENTRYPOINT ["/gopath/bin/gobuster"]