FROM php:7.1-fpm

MAINTAINER Jakub Pistek <mail@jakubpistek.cz>

ENV PHPREDIS_VERSION 3.1.0

RUN apt-get update

# Some basic extensions
RUN docker-php-ext-install -j$(nproc) json mbstring opcache pdo pdo_mysql mysqli

# Redis
RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/$PHPREDIS_VERSION.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts

# Other extensions
RUN apt-get update && apt-get install -y libpq-dev libpng-dev libjpeg-dev libcurl4-openssl-dev \
	&& docker-php-ext-install -j$(nproc) curl gd pdo_pgsql pgsql bcmath iconv mbstring pdo_pgsql pgsql zip redis

ADD wait-for-it.sh /bin/wait-for-it
