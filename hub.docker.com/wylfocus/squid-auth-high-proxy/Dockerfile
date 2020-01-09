FROM ubuntu:16.04

MAINTAINER Wang Yalong <wyl.00@163.com>

RUN apt-get -qqy update
RUN apt-get -qqy upgrade
RUN apt-get -qqy install apache2-utils squid3
RUN mkdir /usr/etc
RUN mkdir -p /etc/squid3/

ENV SQUID_PORT="${SQUID_PORT:-3128}"
ENV SQUID_CONFIG_FILE="${SQUID_CONFIG_FILE:-squid.base.conf}"
ENV SQUID_USERNAME="${SQUID_USERNAME:-name}"
ENV SQUID_PASSWORD="${SQUID_PASSWORD:-password}"

EXPOSE ${SQUID_PORT}:${SQUID_PORT}

VOLUME /var/log/squid3

ADD init /init
#replace the squid config file

ADD ${SQUID_CONFIG_FILE} /etc/squid/squid.conf

CMD ["/init"]
