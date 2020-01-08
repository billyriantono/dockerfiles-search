FROM alpine:3.3

MAINTAINER jsecchiero <looooop@gmail.com>

RUN apk --update add bind &&\
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

EXPOSE 53/udp 53/tcp

RUN mkdir -p /var/cache/bind
CMD ["named", "-c", "/etc/bind/named.conf", "-g", "-u", "named"]
