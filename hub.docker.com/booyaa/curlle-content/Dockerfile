FROM php:5.6.18-fpm

RUN apt-get update && apt-get install -y --no-install-recommends libjpeg-dev libpng12-dev libfreetype6-dev libbz2-dev libmcrypt-dev \
   && apt-get clean && rm -rf /var/lib/apt/lists/* \
   && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-freetype-dir=/usr \
   && docker-php-ext-install bz2 gd mbstring mcrypt opcache zip \
   && rm -rf /usr/src/php
