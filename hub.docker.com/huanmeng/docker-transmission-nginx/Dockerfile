FROM alpine

ADD entrypoint.sh /entrypoint.sh

RUN apk add --no-cache dhcp && \
    mkdir /data && \
    chmod +x /entrypoint.sh && \
    rm /etc/dhcp/dhcpd.conf.example

EXPOSE 67/udp

VOLUME /data
VOLUME /config

ENTRYPOINT [ "/bin/sh", "/entrypoint.sh" ]