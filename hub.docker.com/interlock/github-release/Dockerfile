FROM golang:1.12-alpine as builder

RUN apk update && \
  apk upgrade && \
  apk add git && \
  go get github.com/aktau/github-release && \
  install -d /release && \
  rm -rf /go/src/github.com || true && \
  rm -rf /var/cache/apk/*

COPY bin/* /bin

VOLUME [ "/release" ]

CMD ["/go/bin/github-release"]

