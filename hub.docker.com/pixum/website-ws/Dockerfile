FROM php:5.5-apache

COPY resources/php.ini /usr/local/etc/php/php.ini

COPY resources/sessionvoc.so /php-modules/sessionvoc.so
COPY resources/sessionvoc.ini /usr/local/etc/php/conf.d/sessionvoc.ini

COPY resources/xdebug.so /php-modules/xdebug.so
COPY resources/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN mkdir -p /xdebug/profiler
RUN mkdir -p /xdebug/trace
VOLUME /xdebug

RUN docker-php-ext-install pdo_mysql

RUN ln -sfn /var/source/site/web /var/www/html