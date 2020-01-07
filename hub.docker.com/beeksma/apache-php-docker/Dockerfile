FROM php:7.1-apache
LABEL maintainer "Victor Beek <beeksma@pm.me>"
ENV DEBIAN_FRONTEND noninteractive

# Enable Apache modules
RUN a2enmod proxy proxy_http ssl headers rewrite proxy_wstunnel

# Install PHP extension build dependencies
RUN apt update && apt install -y apt-utils && apt upgrade -y && apt install -y sudo \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libzip-dev \
        libicu-dev \
        mysql-client \
        libmemcached-dev \
        libbz2-dev \
        libav-tools

# Build and configure PHP extensions (apcu, memcache, bz2, mcrypt, gd, pdo_mysql, mysqli, gettext, opcache, zip)
RUN pecl install apcu && \
        docker-php-ext-enable apcu && \
        pecl install memcached && \
        docker-php-ext-enable memcached && \
        docker-php-ext-install bz2 && \
        docker-php-ext-install -j$(nproc) iconv mcrypt && \
        docker-php-ext-install -j$(nproc) intl && \
        docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
        docker-php-ext-install -j$(nproc) gd && \
        docker-php-ext-install pdo_mysql && \
        docker-php-ext-install mysqli && \
        docker-php-ext-install gettext && \
        docker-php-ext-install opcache && \
        docker-php-ext-install zip && \
        echo 'apc.enable_cli=1' >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini

