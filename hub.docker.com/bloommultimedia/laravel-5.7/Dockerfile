FROM php:7.2-fpm

RUN apt-get update && apt-get install -qy unzip git curl libmcrypt-dev mysql-client libpng-dev libjpeg* libfreetype*
RUN yes | pecl install mcrypt-1.0.1
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd
RUN docker-php-ext-enable gd