FROM alpine:3.7

MAINTAINER Nick Alex <bogachev095@gmail.com>

RUN apk update && apk upgrade
RUN apk add apache2-utils squid

RUN mkdir /usr/etc && mkdir -p /etc/squid/

ADD squid.conf /etc/squid/squid.conf

RUN htpasswd -bc /etc/squid/password "${SQUID_USERNAME}" "${SQUID_PASSWORD}"

EXPOSE 3128
VOLUME /var/log/squid

CMD ["squid", "-N"]
