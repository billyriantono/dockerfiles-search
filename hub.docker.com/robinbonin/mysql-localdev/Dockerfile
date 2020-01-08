FROM mysql:5.7

RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y pv;

COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
COPY manage-db.sh /usr/local/bin/manage-db.sh
