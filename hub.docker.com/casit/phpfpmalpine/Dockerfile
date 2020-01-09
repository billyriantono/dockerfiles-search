FROM php:5-fpm-alpine
COPY custom-config.ini /usr/local/etc/php/conf.d
RUN apk upgrade --update && apk add \
        libmcrypt-dev \
        freetype \
	libpng \
        libjpeg-turbo \
	freetype-dev \
        libjpeg-turbo-dev \
        libpng-dev \
    && docker-php-ext-install iconv mcrypt pdo_mysql mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd mysqli 
RUN sed -i -e "s/listen = \[::\]:9000/listen = 0\.0\.0\.0:9000/g" /usr/local/etc/php-fpm.d/zz-docker.conf
