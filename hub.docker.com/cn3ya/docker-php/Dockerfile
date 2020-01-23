FROM php:fpm-alpine
RUN apk add autoconf gcc g++ make \
&& pecl install xdebug redis \
&& docker-php-ext-enable xdebug redis \
&& docker-php-ext-install pdo pdo_mysql \
&& apk del autoconf gcc g++ make
