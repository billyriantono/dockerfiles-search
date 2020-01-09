FROM golang:1.11.0-alpine

ARG GOPROXY_VERSION=master

RUN apk update; apk upgrade; \
    apk add --no-cache git; \
    cd /go/src/; \
    git clone https://github.com/snail007/goproxy.git; \
    cd goproxy; \
    git checkout ${GOPROXY_VERSION}; \
    go get; CGO_ENABLED=0 GOOS=linux go build -ldflags "-s -w" -a -installsuffix cgo -o proxy; \
    chmod 0777 proxy
    
FROM alpine:3.8

LABEL maintainer "Platform/IIBU <zhangzhitao@fmsh.com.cn>"

COPY --from=0 /go/src/goproxy/proxy /usr/bin/proxy
RUN apk update; apk upgrade; \
    apk --no-cache add tzdata bash; \
    mkdir -p /etc/proxy /var/log/proxy; cd /etc/proxy; \
    proxy keygen -C proxy; cd / \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime; echo "Asia/Shanghai" > /etc/timezone 

VOLUME /etc/proxy

CMD proxy ${OPTS}
