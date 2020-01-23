FROM debian:latest

RUN apt-get update && \
   	LC_ALL=C DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
   	 	slapd ldap-utils && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY start /start
RUN chmod 755 /start

VOLUME /var/lib/ldap
VOLUME /etc/ldap/slapd.d

EXPOSE 389 636

CMD ["/start"]
