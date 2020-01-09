FROM	zercle/docker-debian
LABEL	maintainer="Kawin Viriyaprasopsook <bouroo@gmail.com>"

ENV SQUID_VERSION=3.5.23 \
	SQUID_CACHE_DIR=/var/spool/squid \
    SQUID_LOG_DIR=/var/log/squid \
    SQUID_USER=proxy


# Install squid
RUN	apt-get update \
	&& apt-get install -y squid

COPY	./files /
RUN	chmod +x /root/docker-entrypoint.sh

VOLUME	["/var/spool/squid"]

WORKDIR	/root

EXPOSE	3128

ENTRYPOINT ["/root/docker-entrypoint.sh"]
