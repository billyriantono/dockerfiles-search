FROM php:5.5-apache

LABEL maintainer="elliot@yuranga.com"

ENV DATADOG_KEY=8a17a401aa3f0e7e570c88fcddbb404c \
	DEBIAN_FRONTEND=noninteractive

RUN apt update &&  \
	apt install --no-install-recommends -y  \
	libbz2-dev  libmemcached-dev \
	libmemcachedutil2  libmysqlclient-dev  \
	libsasl2-dev libicu-dev  \
	curl git  libmagickwand-dev ghostscript \
	libfreetype6-dev  libjpeg-dev \
	libpng12-dev  libldap2-dev \
	libmcrypt-dev  libpq-dev \
	libxml2-dev  libssh2-1-dev \
	libssh2-1 zbar-tools libc-client-dev libkrb5-dev &&  \
	docker-php-source extract &&  \
	curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/2.2.8.tar.gz &&  \
	tar xfz /tmp/redis.tar.gz &&  \
	rm -r /tmp/redis.tar.gz && \
	mv phpredis-2.2.8 /usr/src/php/ext/redis && \
	pecl install ssh2 memcache imagick imagick-beta &&  \
	docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
	docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
	docker-php-ext-install exif dom mysqli redis gd zip bcmath imap &&  \
	docker-php-ext-enable ssh2 memcache imagick imap && \
	rm -rf /var/lib/apt/lists/* && \
        a2enmod rewrite
COPY --from=ecklerlf2/imagick:latest /usr/bin/convert /usr/local/bin/convert
