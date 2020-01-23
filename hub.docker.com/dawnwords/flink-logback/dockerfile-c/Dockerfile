FROM alpine:latest
MAINTAINER David Manso <david.manso@epistolae.com>

RUN apk --update add keepalived
RUN adduser -S -D keepalived_script
RUN mkdir /config && mkdir /default
RUN mv /etc/keepalived/* /default && rmdir /etc/keepalived && ln -s /config /etc/keepalived

ENTRYPOINT ["/usr/sbin/keepalived", "--dont-fork", "--log-console"]
