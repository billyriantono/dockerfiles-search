FROM php:7.2-apache

MAINTAINER Angel M. Parras <a.m.parras@gmail.com>

################################################################################
# Locales
################################################################################

RUN apt-get update && apt-get install -y locales && apt-get clean

RUN sed -i -e 's/# es_ES ISO-8859-1/es_ES ISO-8859-1/' /etc/locale.gen && \
    sed -i -e 's/# es_ES UTF-8/es_ES UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales

################################################################################
# Mysql + libraries
################################################################################
RUN docker-php-ext-install pdo pdo_mysql gettext

RUN apt-get update && apt-get install -y \
		cron \
		nano \
		git \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		libicu-dev \
		libmcrypt-dev \
	&& docker-php-ext-install -j$(nproc) iconv \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-install -j$(nproc) zip \
	&& docker-php-ext-install -j$(nproc) intl

RUN pecl install mcrypt-1.0.1

RUN docker-php-ext-enable mcrypt

RUN a2enmod rewrite && a2enmod headers

RUN service cron start

################################################################################
# Ports
################################################################################

EXPOSE 80

COPY --from=composer /usr/bin/composer /usr/bin/composer