# Base image
ARG PHP_VERSION=7.2
FROM php:$PHP_VERSION-apache

# Maintainer
MAINTAINER Quentin Buiteman <hello@quentinbuiteman.com>

# Enable modules
RUN a2enmod headers
RUN a2enmod rewrite

# Imagick & GD
RUN apt-get update \
    && apt-get install -y libzip-dev \
    && apt-get install -y zlib1g-dev \
    && apt-get install -y subversion \
    && apt-get install -y --no-install-recommends \
        libmagickwand-dev \
    && rm -rf /var/lib/apt/lists/* \
    && pecl install imagick-beta

# WP CLI
RUN curl https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar > /tmp/wp-cli.phar \
    && chmod +x /tmp/wp-cli.phar \
    && mv /tmp/wp-cli.phar /usr/local/bin/wp

# PHP extensions
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-enable imagick

# Usermods
RUN usermod -u 1000 www-data
RUN usermod -G staff www-data
