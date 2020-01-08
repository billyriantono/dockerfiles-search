FROM php:7.1-apache

MAINTAINER Akkapong Kajornwongwattana<akkapong.kaj@ascendcorp.com>

RUN apt-get update && apt-get install -y \
	wget \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libmemcached-dev \
    zlib1g-dev \
    libltdl7 \
    libltdl-dev \
    libpq-dev \
    libsqlite3-dev \
    git \
    curl \
    libcurl3-dev \
    rsyslog \
    cron \
    unzip \
    libicu-dev \
    --no-install-recommends \
    && docker-php-ext-install -j$(nproc) iconv mcrypt pdo_mysql pdo_pgsql pdo_sqlite zip curl\
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install memcached mongodb redis \
	&& docker-php-ext-enable memcached mongodb redis

#Install composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS http://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

#Install phpunit
RUN wget https://phar.phpunit.de/phpunit-6.2.phar -O /usr/local/bin/phpunit && \
    chmod +x /usr/local/bin/phpunit

# add mod rewrite
RUN a2enmod rewrite

# Clean repository
RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*


