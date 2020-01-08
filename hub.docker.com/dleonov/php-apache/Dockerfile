FROM php:5-apache

RUN set -eux; \
    export DEBIAN_FRONTEND=noninteractive; \
    apt-get update -y; \
    apt-get install -y --no-install-recommends \
        curl \
        ghostscript \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
#        libpng-dev \
        libmcrypt-dev \
        libmagickwand-dev \
        wget; \
    rm -rf /var/lib/apt/lists/*; \
    pecl install \
        xdebug-2.5.5 \
        imagick; \
    docker-php-ext-configure \
        gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
    docker-php-ext-install -j$(nproc) \
        gd \
	mcrypt \
        mysql \
        mysqli \
        pdo \
        pdo_mysql \
        zip; \
    docker-php-ext-enable \
        xdebug \
        imagick; \
    a2enmod \
        rewrite; \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    composer global require "squizlabs/php_codesniffer=*";
    # pear install \
    #     PHP_CodeSniffer;

COPY files /
