FROM php:7.3-fpm-alpine

LABEL maintainer="niccolomeloni@gmail.com"

RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS 

RUN apk add --no-cache \
    git \
    libzip-dev

RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install \
        bcmath \
        zip

RUN pecl install xdebug && \
    docker-php-ext-enable xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN composer global require hirak/prestissimo --no-progress --no-suggest --no-interaction && \
    composer global require laravel/installer --no-progress --no-suggest --no-interaction

RUN apk del -f .build-deps

RUN mkdir /laravel
WORKDIR /laravel