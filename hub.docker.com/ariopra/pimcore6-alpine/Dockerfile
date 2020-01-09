FROM php:7.3-fpm-alpine

LABEL maintainer="ariopra@gmail.com"

RUN apk upgrade --update && apk add --no-cache --virtual .build-deps  \
        alpine-sdk \
        autoconf \
        automake \
        cmake \
        g++ \
        libtool \
    && apk add --no-cache \
        libwebp-dev \
        libjpeg-turbo-dev \
        libjpeg-turbo-utils \
        freetype-dev \
        libmcrypt-dev \
        libpng-dev \
        libxpm-dev \
        icu-dev \
        bzip2-dev \
        libxml2-dev \
        libxslt-dev \
        libzip-dev \
        imagemagick \
        imagemagick-dev \
        graphviz \
        wkhtmltopdf \
    && apk add --no-cache \
        bash \
        shadow \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
        --with-xpm-dir=/usr/include \
        --with-webp-dir=/usr/include/ \
    && docker-php-ext-install intl mysqli bcmath gd bz2 soap xmlrpc xsl pdo_mysql exif zip opcache \
    \
    && pecl config-set php_ini  /usr/local/etc/php/php.ini \
    \
    && pecl install imagick-3.4.4 \
    && docker-php-ext-enable imagick \
    \
    && pecl install apcu \
    && pecl install redis \
    && docker-php-ext-enable redis apcu \
    \
    && cd ~ \
    \
    && git clone https://github.com/google/zopfli.git \
        && cd zopfli \
        && make \
        && cp zopfli /usr/bin/zopflipng \
        && cd .. \
        && rm -rf zopfli \
    \
    && wget http://static.jonof.id.au/dl/kenutils/pngout-20150319-linux.tar.gz \
        && tar -xf pngout-20150319-linux.tar.gz \
        && rm pngout-20150319-linux.tar.gz \
        && cp pngout-20150319-linux/x86_64/pngout /bin/pngout \
        && cd .. \
        && rm -rf pngout-20150319-linux \
    \
    && wget http://prdownloads.sourceforge.net/advancemame/advancecomp-1.17.tar.gz \
        && tar zxvf advancecomp-1.17.tar.gz \
        && cd advancecomp-1.17 \
        && ./configure \
        && make \
        && make install \
        && cd .. \
        && rm -rf advancecomp-1.17 \
    && apk del .build-deps

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_MEMORY_LIMIT -1
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN set -eux; \
    composer global require "hirak/prestissimo:^0.3" --prefer-dist --no-progress --no-suggest --classmap-authoritative; \
    composer clear-cache
ENV PATH="${PATH}:/root/.composer/vendor/bin"

RUN usermod -u 1000 www-data \
    && groupmod -g 1000 www-data

