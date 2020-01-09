FROM php:7-apache
MAINTAINER Alexander Hofbauer <hofbauer.alexander@gmail.com>

WORKDIR /var/www/html

ENV COMPOSER_ALLOW_SUPERUSER 1

#### Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \

## Install stuff
    apt-get update && \
    apt-get install -y --no-install-recommends \
        git-core libxml2-dev libjpeg-dev libpng-dev libxpm-dev libxml2-dev libfreetype6-dev && \
## Enable mod_rewrite
    a2enmod rewrite && \
## add PHP Exension
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install -j$(nproc) \
        ctype \
        dom \
        gd \
        json \
        mbstring \
        session \
        simplexml \
        xml \
        zip && \

    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /usr/src/* && \

#### Install Grav
    composer create-project getgrav/grav ./grav 1.5.* --no-scripts && \
    chmod 777 /var/www/ -R && \
    cd grav && \
    bin/grav install && \
## Install Admin Panel & DevTools
    bin/gpm install -y admin devtools && \
## Doing the permission thing again
    chmod 777 /var/www/ -R && \
    chown www-data:www-data -R /var/www/