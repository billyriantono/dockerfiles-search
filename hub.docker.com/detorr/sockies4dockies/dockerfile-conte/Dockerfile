FROM php:7.2

RUN apt-get update && apt-get install -y unzip git curl libmcrypt-dev mysql-client libreadline-dev libzip-dev curl
RUN yes | pecl install mcrypt-1.0.1
RUN docker-php-ext-install pdo_mysql
RUN pecl install xdebug && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini


RUN curl --silent --show-error https://getcomposer.org/installer | php

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php  --install-dir=bin   --filename=composer
RUN php -r "unlink('composer-setup.php');"



