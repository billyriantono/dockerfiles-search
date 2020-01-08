FROM php:5.6.35-fpm-alpine3.4
RUN apk update && apk add libpng-dev gettext-dev libmcrypt-dev php5-imagick freetype libpng libjpeg-turbo freetype-dev jpeg-dev libjpeg  libjpeg-turbo-dev && docker-php-ext-configure gd --with-freetype-dir=/usr/lib/ --with-png-dir=/usr/lib/ --with-jpeg-dir=/usr/lib/ --with-gd && docker-php-ext-install pdo_mysql mcrypt gettext mysqli gd zip && apk del gcc make && rm -rf /var/cache/apk/*
COPY php.ini /usr/local/etc/php/php.ini
