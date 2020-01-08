FROM php:7.1.3-fpm-alpine
MAINTAINER slanla
RUN apk add --no-cache libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev libmcrypt-dev zip \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-source extract \
    && docker-php-ext-install pdo pdo_mysql mcrypt \
    && docker-php-ext-install -j${NPROC} gd \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev

COPY conf.d/docker-php.ini /usr/local/etc/php/conf.d

EXPOSE 9000
CMD ["php-fpm"]