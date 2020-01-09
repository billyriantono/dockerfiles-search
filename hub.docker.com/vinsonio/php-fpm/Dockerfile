FROM php:7.3-fpm-alpine

RUN apk add --no-cache libpng \
    libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    zlib-dev \
    libxpm-dev

RUN docker-php-ext-install gd pdo pdo_mysql

RUN apk del libpng-dev \
    libjpeg-turbo-dev \
    libwebp-dev \
    zlib-dev \
    libxpm-dev

# COPY ./config/www.conf /usr/local/etc/php-fpm.d/www.conf
# COPY ./config/php-fpm.conf /usr/local/etc/php-fpm.conf
