FROM php:7.2-cli-alpine

MAINTAINER UPX Technologies "labs@upx.com"

RUN apk --no-cache --update add freetype-dev \
        libjpeg-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        git \
        vim \
        curl \
        wget \
        gmp-dev \
        autoconf \
        g++ \
        make
RUN docker-php-ext-install  \
        iconv \
        gmp \
        zip \
        bcmath
RUN pecl install xdebug
RUN docker-php-ext-install sockets
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ENV COMPOSER_ALLOW_SUPERUSER="1" PATH="/root/.composer/vendor/bin:$PATH"

RUN composer global require "phpunit/phpunit=^7.0.0" && \
    composer global require "squizlabs/php_codesniffer=^3.2.2" && \
    composer global require "escapestudios/symfony2-coding-standard=^3.0.1" && \
    composer global require "slevomat/coding-standard=^4.0" && \
    rm -rf /root/.composer/cache && \
    /root/.composer/vendor/bin/phpcs --config-set show_progress 1 && \
    /root/.composer/vendor/bin/phpcs --config-set colors 1 && \
    /root/.composer/vendor/bin/phpcs --config-set report_width 140 && \
    /root/.composer/vendor/bin/phpcs --config-set encoding utf-8 && \
    /root/.composer/vendor/bin/phpcs --config-set installed_paths \
        "/root/.composer/vendor/escapestudios/symfony2-coding-standard,/root/.composer/vendor/slevomat/coding-standard"

COPY xdebug /usr/local/bin/xdebug
RUN chmod +x /usr/local/bin/xdebug
