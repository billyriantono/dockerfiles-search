FROM php:fpm-alpine

MAINTAINER MrGeneral <mrgeneralgoo@gmail.com>

WORKDIR /www

ENV COMPOSER_HOME /composer
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH

# install depends
RUN apk add --no-cache --virtual .persistent-deps \
    oniguruma-dev git freetype-dev libpng-dev libjpeg-turbo-dev libxml2-dev libzip-dev mysql-client \

    && apk add --no-cache --virtual .build-deps $PHPIZE_DEPS \

    # install core extensions
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-configure zip \
    && docker-php-ext-install -j"$(getconf _NPROCESSORS_ONLN)" iconv mbstring pdo_mysql pcntl xml gd zip bcmath \

    # install pecl extensions
    && pecl install redis \
    && docker-php-ext-enable redis \

    # install composer
    && curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && composer global require hirak/prestissimo \

    # clean
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/*
