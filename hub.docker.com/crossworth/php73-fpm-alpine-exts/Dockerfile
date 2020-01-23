FROM php:7.3-fpm-alpine

EXPOSE 9000

RUN apk add --no-cache \
        libzip-dev \
        libpng-dev \
        zip \
        unzip \
        libjpeg-turbo-dev \
        freetype-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install gd bcmath pdo_mysql opcache zip pcntl \
    && docker-php-ext-enable opcache

COPY php-fpm.d/docker.conf /usr/local/etc/php-fpm.d/zz-docker.conf
COPY conf.d/*.ini /usr/local/etc/php/conf.d/
COPY php.ini /usr/local/etc/php/php.ini

CMD ["php-fpm"]