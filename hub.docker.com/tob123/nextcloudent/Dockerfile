FROM ubuntu:bionic
RUN apt-get update \
    && apt-get install -y freeradius freeradius-ldap ldap-utils ca-certificates \
    && cp -a /etc/freeradius /etc/freeradius-dist
COPY entrypoint.sh /entrypoint.sh

CMD ["/entrypoint.sh"]
EXPOSE 1812/udp 1813/udp
