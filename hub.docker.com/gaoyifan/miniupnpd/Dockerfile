FROM smartentry/debian:9-0.4.1

MAINTAINER Yifan Gao <docker@yfgao.com>

ADD . $ASSETS_DIR

RUN smartentry.sh build

ENV UPNP_LAN=eth0 \
    UPNP_LAN_CIDR=192.168.1.0 \
    UPNP_SECURE_MODE=yes \
    UPNP_WAN_INTERFACE=eth1

CMD ["/usr/sbin/miniupnpd", "-d", "-f", "/etc/miniupnpd/miniupnpd.conf"]
