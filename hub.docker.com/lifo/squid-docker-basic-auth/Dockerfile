FROM alpine:3.7

MAINTAINER Nick Alex <bogachev095@gmail.com>

RUN apk update && apk upgrade
RUN apk add apache2-utils squid
RUN mkdir /usr/etc && mkdir -p /etc/squid3/

EXPOSE 3128
VOLUME /var/log/squid3

ADD init /init
ADD squid.conf /etc/squid/squid.conf

CMD ["/init"]
