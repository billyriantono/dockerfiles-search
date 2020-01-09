FROM debian:8
ENV DEBIAN_FRONTEND noninteractive

EXPOSE 3128
VOLUME /var/log/squid3
VOLUME /var/spool/squid3

ENTRYPOINT ["/docker-entrypoint.sh"]

RUN apt-get -qq update && apt-get -qq -y --no-install-recommends install squid3

COPY docker-entrypoint.sh /docker-entrypoint.sh
COPY squid.conf /etc/squid3/squid.conf
