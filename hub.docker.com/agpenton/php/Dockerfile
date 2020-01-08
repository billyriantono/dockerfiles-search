FROM php:latest
LABEL maintainer="Asdrubal Gonzalez"
ENV container=docker
RUN apt-get update -yqq && curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -yqq \
git \
nodejs
RUN apt-get install -yqq libcurl4-gnutls-dev \
libicu-dev \
libmcrypt-dev \
libvpx-dev \
libjpeg-dev \
libpng-dev \
libxpm-dev \
libfreetype6-dev \
libexpat1-dev \
libgmp3-dev \
libldap2-dev \
unixodbc-dev \
libpq-dev \
libaspell-dev \
libsnmp-dev \
libpcre3-dev \
libtidy-dev \
libxml2-dev \
libzip-dev \
libbz2-dev \
&& rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo_mysql json intl gd xml zip bz2 opcache \
&& pecl install xdebug \
&& docker-php-ext-enable xdebug
RUN curl -sS https://getcomposer.org/installer | php \
&& php composer.phar \
&& npm install \
&& npm i -g phplint

