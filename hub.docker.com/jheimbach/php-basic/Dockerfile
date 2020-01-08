FROM php:7.2-fpm

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng-dev \
		ca-certificates \
		curl \
		git \
		libzip-dev \
		zip \
		unzip \
	&& rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-install pdo_mysql json opcache zip

RUN sed -ri 's/^www-data:x:33:33:/www-data:x:1000:100:/' /etc/passwd

ARG PHP_INI=./php.ini
ARG PHP_CONF_FILE=$PHP_INI_DIR/php.ini

COPY $PHP_INI $PHP_CONF_FILE

COPY local_settings /usr/local/bin/php_local_settings

ENV PHP_CONF_FILE=$PHP_CONF_FILE \
    PHP_MAX_EXECUTION_TIME="60" \
    PHP_MAX_INPUT_TIME="60" \
    PHP_MEMORY_LIMIT="512M" \
    PHP_ERROR_REPORTING="E_ALL" \
    PHP_DISPLAY_ERRORS="On" \
    PHP_DISPLAY_STARTUP_ERRORS="On" \
    PHP_POST_MAX_SIZE="64M" \
    PHP_UPLOAD_MAX_FILESIZE="64M" \
    PHP_DATE_TIMEZONE="Europe\/Berlin"


RUN php_local_settings
