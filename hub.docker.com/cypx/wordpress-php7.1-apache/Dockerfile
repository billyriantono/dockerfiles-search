FROM wordpress:php7.1-apache

RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		mysql-client \
	; \
	apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false; \
	rm -rf /var/lib/apt/lists/*