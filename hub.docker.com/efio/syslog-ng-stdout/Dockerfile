FROM alpine:3.4
MAINTAINER Kristian Martensen <kristian@efio.dk>

RUN apk add --no-cache syslog-ng \
 && mkdir /sidecar \
 && rm -f /etc/syslog-ng/*

COPY syslog-ng.conf /etc/syslog-ng/
VOLUME ["/sidecar"]

CMD ["syslog-ng", "-F"]
