FROM smartentry/centos:7-0.4.1

MAINTAINER Yifan Gao <docker@yfgao.com>

COPY . $ASSETS_DIR

RUN smartentry.sh build

CMD ["/usr/sbin/squid", "-N", "-f", "/etc/squid/squid.conf"]
