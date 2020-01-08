FROM php:7

RUN curl -sS https://getcomposer.org/installer | \
		php -- --install-dir=/usr/local/bin/ --filename=composer \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		git \
		unzip \
	&& rm -rf /var/lib/apt/lists/*
