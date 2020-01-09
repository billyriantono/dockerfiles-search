FROM sameersbn/squid:3.5.27

RUN apt-get update && apt-get install -y iproute2 apache2-utils

COPY no_auth_squid.conf /etc/squid
COPY auth_squid.conf /etc/squid

COPY setup.sh /sbin/setup.sh
RUN chmod 755 /sbin/setup.sh

ENV KAOS_PROXY_LATENCY=0 \
		KAOS_PROXY_JITTER=0

ENTRYPOINT ["sh", "-c", "/sbin/setup.sh ; /sbin/entrypoint.sh"]
