FROM php:7.1-fpm-alpine

RUN docker-php-ext-install opcache && docker-php-ext-enable opcache

RUN apk add --update \
	autoconf \
	gcc \
	libc-dev \
	make \
	git \
	&& rm -rf /var/cache/apk/*

RUN pecl install xdebug

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN composer global require hirak/prestissimo
