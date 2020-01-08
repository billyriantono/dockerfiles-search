FROM php:5.6-fpm

RUN apt-get update && apt-get install -y \
      rsync \
      libxml++2.6-dev \
      libmcrypt-dev \
    && pecl install redis \
    && docker-php-ext-install mysqli soap mcrypt opcache \
    && docker-php-ext-enable redis \
    && sed -E -i 's/^(pm\.max_children)\s+=\s+[0-9]+/\1=32/' /usr/local/etc/php-fpm.d/www.conf \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
