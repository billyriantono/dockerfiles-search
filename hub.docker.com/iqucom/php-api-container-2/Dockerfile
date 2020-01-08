FROM php:7-fpm

MAINTAINER mauriciovander@gmail.com

ENV LC_ALL          C.UTF-8
ENV LANG            en_US.UTF-8
ENV LANGUAGE        en_US.UTF-8

# Dependencies
RUN apt-get update
RUN apt-get autoremove -y

RUN apt-get install -y git wget nano libmcrypt-dev libpng12-dev libjpeg-dev libpq-dev curl phing libxml2-dev libsqlite3-dev libicu-dev libfreetype6-dev libjpeg62-turbo-dev libcurl4-gnutls-dev libbz2-dev libssl-dev
RUN rm -rf /var/lib/apt/lists/* 

RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr
RUN docker-php-ext-install gd

# Install PECL extensions
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

RUN pecl install phar
RUN docker-php-ext-install phar

RUN pecl install intl
RUN docker-php-ext-install intl

RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install mbstring 
RUN docker-php-ext-install zip 
RUN docker-php-ext-install soap 

RUN pear install --alldeps Mail
RUN rm -rf /tmp/pear

RUN pecl install mongodb

RUN echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini
RUN echo "extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini

EXPOSE 9000

