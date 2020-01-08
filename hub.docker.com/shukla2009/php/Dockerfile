FROM php:7.1.9-apache

RUN apt-get update
RUN apt-get -y install pkg-config libssl-dev
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install zip
RUN curl -s https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

#for debugging
RUN yes | pecl install xdebug
RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN a2enmod rewrite