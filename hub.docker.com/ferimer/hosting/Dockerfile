FROM php:7-apache
MAINTAINER <devteam@ferimer.es>

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli pdo_mysql

RUN apt update && \
    apt dist-upgrade -y && \
    apt install -y libzip-dev libxml2-dev && \
    apt autoremove -y && \
    docker-php-ext-install zip intl xmlrpc soap opcache

RUN mkdir /var/www/moodledata
VOLUME /var/www/moodledata

ADD https://download.moodle.org/download.php/direct/stable37/moodle-latest-37.tgz /opt
RUN tar xvzf /opt/moodle-latest-37.tgz --strip 1 && rm /opt/moodle-latest-37.tgz && chown -R www-data:www-data /var/www/
VOLUME /var/www/html


