FROM alpine:3.6
RUN apk add --no-cache syslog-ng
EXPOSE 514/udp 601/tcp 6514/tcp
ENTRYPOINT ["/usr/sbin/syslog-ng", "-F"]
