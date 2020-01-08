FROM php:7.1-fpm

RUN apt-get update && \
    apt-get install -y --no-install-recommends git zip unzip libpng-dev libjpeg-dev

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install mysqli pdo_mysql gd pcntl zip

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/ && \
    ln -s /usr/local/bin/composer.phar /usr/local/bin/composer
