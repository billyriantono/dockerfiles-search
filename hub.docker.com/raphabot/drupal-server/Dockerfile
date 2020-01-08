FROM php:5.6.6-apache
MAINTAINER Raphael Bottino <raphabot@gmail.com>

RUN apt-get update -y && apt-get install -y \
        curl libcurl3 libcurl3-dbg libcurl4-openssl-dev libmcrypt-dev libjpeg-dev libpng-dev libfreetype6-dev php-apc php5-gd php5-curl php5-memcache memcached


RUN docker-php-ext-install iconv mcrypt
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install pdo pdo_mysql curl gd
RUN docker-php-ext-install mysql mysqli

RUN sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf #sites-available/default
RUN a2enmod rewrite vhost_alias
