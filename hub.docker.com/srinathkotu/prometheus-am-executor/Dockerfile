FROM golang:alpine as builder
MAINTAINER Martin Baillie <martin.t.baillie@gmail.com>

WORKDIR /go/src/github.com/imgix/prometheus-am-executor
COPY ${PWD} .
RUN apk --no-cache --virtual .build-deps add go git\
	&& go get -u github.com/prometheus/alertmanager/... \
        && go get -u github.com/prometheus/client_golang/... \
        && CGO_ENABLED=0 GOARCH=amd64 GOOS=linux \
        go build -a -installsuffix cgo -ldflags '-s -w -extld ld -extldflags -static'

FROM ubuntu:16.04
WORKDIR /
CMD bash
RUN apt-get -y update && apt-get -y install curl && curl -sSL https://get.docker.com/ | sh
RUN curl -L https://github.com/docker/compose/releases/download/1.18.0/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose && chmod +x /usr/bin/docker-compose
COPY --from=builder /go/src/github.com/imgix/prometheus-am-executor/prometheus-am-executor .
ENTRYPOINT ["/prometheus-am-executor"]
