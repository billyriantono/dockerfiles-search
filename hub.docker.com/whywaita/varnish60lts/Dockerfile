FROM ubuntu:18.04

MAINTAINER whywaita <https://github.com/whywaita>

RUN apt update -qq -y \
    && apt install -y curl

RUN curl -s https://packagecloud.io/install/repositories/varnishcache/varnish60lts/script.deb.sh | bash \
    && apt install -y varnish

VOLUME ["/etc/varnish"]
WORKDIR /etc/varnish

EXPOSE 80
CMD /usr/sbin/varnishd -F -f /etc/varnish/default.vcl -a :80 -s malloc,128m
