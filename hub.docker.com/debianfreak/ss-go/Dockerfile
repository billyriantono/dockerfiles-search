#2018-12-10 v0.11 test2
FROM golang:1.10.3-alpine3.8 AS builder

RUN apk upgrade --update \
    && apk add git \
    && go get github.com/shadowsocks/go-shadowsocks2

FROM alpine:3.8

LABEL maintainer="FRANK <https://github.com/frankpen>"

ARG TZ="Asia/Shanghai"

ENV TZ ${TZ}

RUN apk upgrade --update \
    && apk add bash tzdata \
    && ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime \
    && echo ${TZ} > /etc/timezone \
    && rm -rf /var/cache/apk/*

COPY --from=builder /go/bin/go-shadowsocks2 /usr/bin/ss-go
ENV ARGS="ss://AES-128-CFB:password@1.2.3.4:10400" 
EXPOSE 4080/tcp 4080/udp
CMD /usr/bin/ss-go -c ${ARGS} -verbose -socks :4080

