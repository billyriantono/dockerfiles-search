FROM php:7.2.4-fpm-alpine3.7
RUN apk update && apk add php7-mysqlnd php7-imagick libpng-dev gettext-dev libmcrypt-dev freetype libpng libjpeg-turbo freetype-dev jpeg-dev libjpeg  libjpeg-turbo-dev && docker-php-ext-configure gd --with-freetype-dir=/usr/lib/ --with-png-dir=/usr/lib/ --with-jpeg-dir=/usr/lib/ --with-gd && docker-php-ext-install pdo_mysql gettext mysqli gd zip && apk del gcc make && rm -rf /var/cache/apk/*
COPY php.ini /usr/local/etc/php/php.ini
