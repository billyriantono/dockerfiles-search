FROM php:7.1-apache-jessie

LABEL maintainer="https://github.com/dcb9"

RUN docker-php-ext-install opcache

COPY opcache.ini /usr/local/etc/php/conf.d/opcache.ini
COPY apache.conf /etc/apache2/sites-enabled/000-default.conf

ENV PHP_OPCACHE_ENABLE="0"

RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd zip pdo_mysql fileinfo \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && rm -rf composer-setup.php \
    && a2enmod rewrite
