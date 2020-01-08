FROM	mediawiki:1.31.3

RUN	apt-get update -y && \
	apt-get install -y libpq-dev && \
	docker-php-ext-install pgsql && \
	apt-get remove -y libpq-dev && \
	apt-get clean -y

