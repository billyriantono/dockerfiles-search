FROM alpine:edge

RUN apk add --update \
    transmission-daemon \
    && rm -rf /var/cache/apk/*

RUN mkdir -p /transmission/downloads \
  && mkdir -p /transmission/incomplete \
  && mkdir -p /etc/transmission-daemon

RUN [ -f /etc/transmission-daemon/settings.json ] && echo "Transmission settings file exists." || (/usr/bin/transmission-daemon -d 2>&1 | sed 's/\(rpc-\(host-\)\?whitelist-enabled":\) true/\1 false/g' > /etc/transmission-daemon/settings.json)

VOLUME ["/etc/transmission-daemon"]
VOLUME ["/transmission/downloads"]
VOLUME ["/transmission/incomplete"]

EXPOSE 9091 51413/tcp 51413/udp

ENTRYPOINT ["/usr/bin/transmission-daemon","--foreground","--config-dir","/etc/transmission-daemon","--incomplete-dir","/transmission/incomplete","--download-dir","/transmission/downloads","--log-debug"]
