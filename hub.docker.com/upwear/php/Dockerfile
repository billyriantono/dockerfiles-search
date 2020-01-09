FROM php:7-fpm-alpine
COPY fpm.conf /usr/local/etc/php-fpm.d/zz-root.conf
COPY php.ini /usr/local/etc/php/conf.d/php.ini

RUN set -xe \
&& apk --no-cache add libpng-dev libjpeg-turbo-dev freetype-dev \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install mysqli opcache gd

CMD ["php-fpm", "-R"]
