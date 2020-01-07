FROM golang:alpine AS builder
MAINTAINER Roger Cui <itabas016@gmail.com>

COPY . /tmp/repo
RUN set -ex \
 # Build environment setup
 && apk add --no-cache --virtual .build-deps \
     bash \ 
     git \
 && cd /tmp/repo \
 && git clone --recursive https://github.com/shadowsocks/shadowsocks-go.git \
 && cd shadowsocks-go \
 && CGO_ENABLED=0 go get github.com/shadowsocks/shadowsocks-go/cmd/shadowsocks-server \
 && apk del .build-deps \
 && rm -rf /tmp/repo

FROM scratch

COPY --from=builder /etc/passwd /etc/passwd
COPY --from=builder /go/bin/shadowsocks-server /usr/local/bin/

USER nobody

ENTRYPOINT [ "/usr/local/bin/shadowsocks-server" ]