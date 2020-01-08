
FROM php:7.2.11-fpm-alpine3.8

RUN apk add --no-cache --update postgresql-dev && \
	apk add --no-cache --virtual .phpize-deps $PHPIZE_DEPS linux-headers && \
	pecl install redis && \
	docker-php-ext-enable redis && \
	docker-php-ext-install pdo pdo_pgsql && \
	docker-php-source delete && \
	apk del .phpize-deps && \
	rm -rf /var/cache/apk/*
	
COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/php-fpm.conf
