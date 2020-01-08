FROM php:7.3-fpm-alpine

RUN apk update && apk add --no-cache --virtual .build-deps \
       autoconf \
       g++ \
       libtool \
       make \
       pcre-dev \
    && apk add --no-cache \
       postgresql-dev \
       freetype-dev \
       libpng-dev \
       tzdata \
       unzip \
       imagemagick-dev \
       libintl \
       libzip-dev \
       icu \
       icu-dev \
       libxml2-dev \
       gettext-dev \
       freetype-dev \
       libjpeg-turbo-dev \
       libmcrypt-dev \
       openssl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install gd pdo_mysql mysqli pgsql pdo_pgsql opcache zip xmlrpc exif bcmath intl zip soap iconv gettext sockets pdo mbstring \
    && pecl install imagick \
    && pecl install xdebug-beta \
	&& docker-php-ext-enable imagick xdebug \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apk del .build-deps

COPY php.ini /usr/local/etc/php/php.ini

CMD ["php-fpm"]