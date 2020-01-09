FROM debian:stretch-slim

RUN apt-get update \
	&& apt-get install -y \
		php \
		php-mbstring \
		php-curl \
		php-json \
		php-pgsql \
		php-mcrypt \
		php-xml \
	&& rm -rf /var/lib/apt/lists/*

