FROM golang:1.9.1-alpine as builder
MAINTAINER easylo <easylo@users.noreply.github.com>

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go
ENV CGO_ENABLED=0

COPY . $GOPATH/src/github.com/easylo/prometheus-bind-exporter
WORKDIR $GOPATH/src/github.com/easylo/prometheus-bind-exporter

RUN apk add --update --no-cache \
       make \
       git \
       ca-certificates
      
RUN make build

FROM        quay.io/prometheus/busybox:latest

COPY --from=builder /go/src/github.com/easylo/prometheus-bind-exporter/prometheus-bind-exporter /bin/prometheus-bind-exporter

EXPOSE      9119
ENTRYPOINT  [ "/bin/prometheus-bind-exporter", "-bind.stats-groups", "server,view,tasks"]
