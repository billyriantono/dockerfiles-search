FROM php:7.1-fpm-alpine

ENV PHP_EXTENSIONS pdo pdo_mysql mbstring curl gd intl json mcrypt soap zip xml gettext bcmath exif

ENV MEMCACHED_DEPS zlib-dev libmemcached-dev cyrus-sasl-dev
RUN apk add --no-cache --update \
    libmemcached-libs zlib curl-dev zip \
    libpng-dev icu-dev libmcrypt-dev libzip-dev \
    libxml2-dev gettext-dev libjpeg-turbo-dev jpeg-dev freetype-dev exiftool

RUN set -xe \
    && apk add --no-cache --update --virtual .phpize-deps $PHPIZE_DEPS \
    && apk add --no-cache --update --virtual .memcached-deps $MEMCACHED_DEPS \
    && pecl install memcached xdebug \
    && rm -rf /usr/share/php7 \
    && rm -rf /tmp/* \
    && apk del .memcached-deps .phpize-deps

RUN mv "$PHP_INI_DIR/php.ini-development" "/usr/local/etc/php/php.ini"

RUN docker-php-ext-configure gd \
--with-freetype-dir=/usr/include/ \
--with-jpeg-dir=/usr/include/

RUN docker-php-ext-install ${PHP_EXTENSIONS}

# Composer installation needs to be done before installing xdebug. Otherwise installation hangs.
COPY ./install-composer.sh install-composer.sh
RUN sh install-composer.sh

RUN docker-php-ext-enable memcached xdebug

RUN { \
		echo "xdebug.remote_enable=1"; \
		echo "xdebug.remote_autostart=1"; \
		echo "xdebug.remote_port=9001"; \
		echo "xdebug.remote_connect_back=0"; \
		echo "xdebug.remote_host=10.254.254.254"; \
	} >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

WORKDIR "/var/app/current"
