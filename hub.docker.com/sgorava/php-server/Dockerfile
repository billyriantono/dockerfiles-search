FROM php:5.6-apache
MAINTAINER Juraj Oravec <juraj.oravec@shopsys.com>

ENV DEBIAN_FRONTEND noninteractive

# Common
RUN apt-get update && \
  apt-get install -y \
    openssl \
    git \
    curl


# PHP
## intl
RUN apt-get update && \
  apt-get install -y libicu-dev && \
  docker-php-ext-configure intl && \
  docker-php-ext-install intl

## images
RUN apt-get update \
  && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng12-dev \
    libgd-dev && \
  docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
  docker-php-ext-install \
    gd \
    exif

## xml
RUN apt-get update && \
  apt-get install -y \
    libxml2-dev \
    libxslt-dev && \
  docker-php-ext-install \
    dom \
    xmlrpc \
    xsl

## database
RUN \
  docker-php-ext-configure mysql --with-mysql=mysqlnd && \
  docker-php-ext-configure mysqli --with-mysqli=mysqlnd && \
  docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
  docker-php-ext-install \
    mysql \
    mysqli \
    pdo_mysql

## mcrypt
RUN apt-get update && \
  apt-get install -y \
    libmcrypt-dev && \
  docker-php-ext-install mcrypt

## strings
RUN docker-php-ext-install \
  gettext \
  mbstring \
  iconv

## math
RUN apt-get update && \
  apt-get install -y \
    libgmp-dev && \
  ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/include/gmp.h && \
  docker-php-ext-install \
    gmp \
    bcmath

## compression
RUN apt-get update && \
  apt-get install -y \
    libbz2-dev \
    zlib1g-dev && \
  docker-php-ext-install \
    zip \
    bz2

## ftp
RUN apt-get update && \
  apt-get install -y \
    libssl-dev && \
  docker-php-ext-install \
    ftp

## curl
RUN apt-get update && \
  apt-get install -y \
    libcurl4-openssl-dev && \
  docker-php-ext-install \
    curl

## others
RUN docker-php-ext-install \
  calendar \
  phar \
  soap \
  sockets \
  sysvmsg \
  sysvsem \
  sysvshm

## Install composer and put binary into $PATH
RUN curl -sS https://getcomposer.org/installer | php && \
  mv composer.phar /usr/local/bin/ && \
  ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

## npm
RUN apt-get update && \
  apt-get install -y \
    npm

## Install Grunt globally
RUN npm install -g grunt-cli


# Configure
ENV LOCALTIME Europe/Bratislava

ENV HTTPD_CONF_DIR /etc/apache2/conf-enabled/
ENV HTTPD__DocumentRoot /var/www/html

ENV PHP_INI_DIR /usr/local/etc/php

RUN sed -i "s/DocumentRoot.*/DocumentRoot \${HTTPD__DocumentRoot}/"  /etc/apache2/apache2.conf

EXPOSE 80
EXPOSE 443

COPY docker-entrypoint.sh /entrypoint.sh

WORKDIR /var/www

ENTRYPOINT ["/entrypoint.sh"]


# Clean
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/*
