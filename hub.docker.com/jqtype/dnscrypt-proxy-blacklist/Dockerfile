FROM golang:1.13-alpine as build

LABEL maintainer "Jun Kurihara <kurihara@ieee.org>"

RUN apk --no-cache add git && \
    git clone https://github.com/junkurihara/dnscrypt-proxy.git /go/src/github.com/jedisct1/ && \
    cd /go/src/github.com/jedisct1/dnscrypt-proxy && \
    git checkout filter_nxdomain && \
    CGO_ENABLED=0 GOOS=linux go install -a -ldflags '-s -w -extldflags "-static"' -v ./...

FROM alpine:latest

RUN apk --no-cache add ca-certificates python2 git

COPY --from=build /go/bin/dnscrypt-proxy /usr/local/bin/dnscrypt-proxy
COPY --from=build /go/src/github.com/jedisct1/utils/generate-domains-blacklists/generate-domains-blacklist.py /usr/local/bin/generate-domains-blacklist.py
COPY ./docker-bin/* /usr/local/bin/

RUN chmod 755 /usr/local/bin/*

VOLUME /config
VOLUME /var/log/dnscrypt-proxy

EXPOSE 53/tcp 53/udp

CMD ["/usr/local/bin/start.sh"]


