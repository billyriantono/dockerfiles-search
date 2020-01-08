# Docker file for the Utrecht Trouwplanner API

# GET AN APACHE IMAGE
FROM php:7.2-apache

# Request system packages
RUN apt-get update && apt-get install --no-install-recommends -y \
	curl \
    libpng-dev \
    libjpeg-dev \
    wget \
    git \
    unzip \
    gettext \
    imagemagick \
	acl \
	file \
&& rm -rf /var/lib/apt/lists/*

# Enable rewite rules
RUN a2enmod rewrite

# Copy apache configuration
COPY ./docker/000-default.conf /etc/apache2/sites-available

# PHP extensions
RUN docker-php-ext-install mysqli gd mbstring

# PHP configuration
# @todo
# COPY ./docker/php.ini /usr/local/etc/php/php.ini

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN ln -s $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini
COPY docker/php/api-platform.ini $PHP_INI_DIR/conf.d/

# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN set -eux; \
	composer global require "hirak/prestissimo:^0.3" --prefer-dist --no-progress --no-suggest --classmap-authoritative; \
	composer clear-cache
ENV PATH="${PATH}:/root/.composer/vendor/bin"

WORKDIR /srv/api

# build for production
ARG APP_ENV=prod

# prevent the reinstallation of vendors at every changes in the source code
COPY composer.json composer.lock symfony.lock ./
RUN set -eux; \
	composer install --prefer-dist --no-dev --no-autoloader --no-scripts --no-progress --no-suggest; \
	composer clear-cache

# copy only specifically what we need
COPY bin bin/
COPY config config/
COPY public public/
COPY src src/

RUN set -eux; \
	mkdir -p var/cache var/log; \
	composer dump-autoload --classmap-authoritative --no-dev; \
	composer run-script --no-dev post-install-cmd; \
	chmod +x bin/console; sync
VOLUME /srv/api/var
