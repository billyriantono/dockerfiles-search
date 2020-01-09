FROM alpine:latest

MAINTAINER infra@coldfilter.io

RUN apk --update upgrade && \
    apk add --update bind && \
    rm -rf /var/cache/apk/*

WORKDIR /etc/bind
COPY etc/bind/ /etc/bind/
COPY var/named/ /var/named/

VOLUME ["/etc/bind", "/var/log/named"]

EXPOSE 53/tcp
EXPOSE 53/udp

CMD ["/usr/sbin/named", "-c", "/etc/bind/named.conf", "-f"]
