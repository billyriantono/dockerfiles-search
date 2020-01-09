FROM php:7.2-fpm
COPY --from=composer:1.5 /usr/bin/composer /usr/bin/composer
COPY php.ini /usr/local/etc/php/
RUN apt-get update && apt-get install -y git \
 ssh \
 zlib1g-dev \
 libfreetype6-dev \
 libjpeg62-turbo-dev \
 libmcrypt-dev \
 libpng-dev \
        && docker-php-ext-install -j$(nproc) zip pdo_mysql \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) gd