FROM alpine:latest
MAINTAINER plmu

RUN apk add --no-cache transmission-daemon dumb-init \
    && mkdir -p /share/CE_CACHEDEV1_DATA/Download/transmission \
    && ln -s /mnt/complete /share/CE_CACHEDEV1_DATA/Download/transmission/completed

ENV TRANSMISSION_HOME /mnt/config

VOLUME /mnt

EXPOSE 9091 51423 51423/udp

ENTRYPOINT ["/usr/bin/dumb-init", "--", "/usr/bin/transmission-daemon","-f"]
