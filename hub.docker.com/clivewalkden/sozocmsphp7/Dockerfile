FROM php:7-fpm

RUN apt-get update && \
    apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev && \
    docker-php-ext-install -j$(nproc) mysqli pdo_mysql iconv && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) gd

# Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/bin/composer