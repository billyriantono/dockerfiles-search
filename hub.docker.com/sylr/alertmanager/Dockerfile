FROM golang:1.13-alpine3.10 AS builder

ADD . /go/src/github.com/prometheus/alertmanager
WORKDIR /go/src/github.com/prometheus/alertmanager

RUN apk update && apk upgrade && apk add --no-cache git alpine-sdk

RUN make build

FROM        prom/busybox:latest
MAINTAINER  The Prometheus Authors <prometheus-developers@googlegroups.com>

COPY  --from=builder /go/src/github.com/prometheus/alertmanager/amtool                       /bin/amtool
COPY  --from=builder /go/src/github.com/prometheus/alertmanager/alertmanager                 /bin/alertmanager
COPY  --from=builder /go/src/github.com/prometheus/alertmanager/examples/ha/alertmanager.yml /etc/alertmanager/alertmanager.yml

EXPOSE     9093
VOLUME     [ "/alertmanager" ]
WORKDIR    /etc/alertmanager
ENTRYPOINT [ "/bin/alertmanager" ]
CMD        [ "--storage.path=/alertmanager" ]
