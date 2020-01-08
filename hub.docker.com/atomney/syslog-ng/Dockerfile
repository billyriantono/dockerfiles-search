FROM alpine:latest

MAINTAINER atomney <atomney+docker@gmail.com>

RUN apk update && \
    apk add syslog-ng && \
    ln -s /var/log /data

COPY syslog-ng.conf /etc/syslog-ng/syslog-ng.conf

EXPOSE 514/tcp 514/udp

VOLUME ["/data"]

CMD ["/usr/sbin/syslog-ng", "-F", "-f", "/etc/syslog-ng/syslog-ng.conf"]
