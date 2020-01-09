## LAMP with PHP 7.2
FROM php:5.6-apache
LABEL MAINTAINER="Francesco Bianco <info@javanile.org>"
WORKDIR /var/www/html

## Settings
ENV MB_SRC=http://sourceforge.net/projects/phpmybackup/files/phpMyBackupPro
ENV MB_VER=2.5
ENV PHP_MEMORY_LIMIT=32M
ENV PHP_MAX_EXECUTION_TIME=30

## Install dependencies
RUN apt-get update \
 && apt-get install -y --no-install-recommends unzip \
 && docker-php-ext-install mysql \
 && rm -rf /var/lib/apt/lists/*
COPY php.ini /usr/local/etc/php/php.ini

## Download
RUN curl -o mb.zip -SL ${MB_SRC}/phpMyBackupPro%20${MB_VER}/phpMyBackupPro-${MB_VER}.zip \
 && unzip -q mb && rm mb.zip && mv phpMyBackupPro-${MB_VER} mybackup \
 && mv mybackup/definitions.php mybackup/definitions.override.php \
 && chmod 777 mybackup/global_conf.php mybackup/export
COPY definitions.php mybackup/definitions.php

## Running
COPY foreground.sh /usr/local/bin/
CMD ["foreground.sh"]
