FROM php:7.1.1-fpm-alpine
MAINTAINER billypon

RUN apk add --no-cache \
        libintl icu-libs libmcrypt libbz2 libpng libjpeg-turbo libwebp freetype \
        gettext-dev icu-dev libmcrypt-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
		openssl \
		openldap openldap-dev \

    && docker-php-ext-configure gd --with-jpeg-dir=/usr/include --with-webp-dir=/usr/include --with-freetype-dir=usr/include \
    && docker-php-ext-configure ldap \
    && pecl bundle -d /usr/src/php/ext redis \
    && docker-php-ext-install bcmath bz2 calendar exif gd gettext intl mcrypt mysqli pdo_mysql pcntl sockets zip redis ldap \

    && apk del \
        gettext-dev icu-dev libmcrypt-dev zlib-dev bzip2-dev \
        libpng-dev libjpeg-turbo-dev libwebp-dev freetype-dev \
		openldap-dev \
    
    && rm -rf /tmp/pear/cache
