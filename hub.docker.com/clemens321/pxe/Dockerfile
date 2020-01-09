FROM alpine:${ALPINE_VERSION:-3.10}

MAINTAINER Clemens Brauers <clemens321@admin-cb.de>

RUN apk --no-cache add dnsmasq

COPY entry-pxe.sh /entry-pxe.sh

ENTRYPOINT ["/entry-pxe.sh"]
