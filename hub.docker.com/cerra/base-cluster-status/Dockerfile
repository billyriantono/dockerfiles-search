FROM golang:1.9.2 AS builder

WORKDIR /go/src/github.com/cerra-io/base-cluster-status/

COPY main.go .
COPY ./vendor ./vendor

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o cluster-status .

FROM alpine:latest
MAINTAINER 	Ali Al-Shabibi <ali#cerra.io>

RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*
COPY --from=builder /go/src/github.com/cerra-io/base-cluster-status/cluster-status .

CMD [ "./cluster-status", "server" ]
