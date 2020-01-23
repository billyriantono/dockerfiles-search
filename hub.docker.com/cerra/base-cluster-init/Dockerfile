FROM golang:1.9.2 AS builder

WORKDIR /go/src/github.com/cerra-io/base-cluster-init/

COPY main.go .
COPY ./cmd ./cmd
COPY ./manager ./manager
COPY ./vendor ./vendor
COPY ./worker ./worker
COPY ./utils ./utils

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o cluster-init .

FROM alpine:latest
MAINTAINER 	Ali Al-Shabibi <ali#cerra.io>

RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*
COPY --from=builder /go/src/github.com/cerra-io/base-cluster-init/cluster-init .

CMD [ "./cluster-init", "server" ]
