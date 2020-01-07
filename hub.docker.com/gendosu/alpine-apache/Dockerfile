# alpine-base
#
# VERSION               0.0.1

FROM      gendosu/alpine-base:latest

MAINTAINER Gen Takahashi <gendosu@gmail.com>

RUN apk add --update \
    apache2 \
&&  rm -rf /var/cache/apk/*

RUN mkdir -p /run/apache2

CMD rm -rf /run/apache2/* || true && /usr/sbin/httpd -DFOREGROUND
