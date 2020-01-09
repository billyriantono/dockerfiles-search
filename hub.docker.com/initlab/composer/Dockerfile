FROM php:5.6-cli
MAINTAINER Roman Agabekov <r.agabekov@gmail.com>

RUN apt-get update && apt-get install -y git
RUN echo "date.timezone = UTC" >> /usr/local/etc/php/php.ini
RUN echo "memory_limit = -1" >> /usr/local/etc/php/php.ini

RUN php -r "readfile('https://getcomposer.org/installer');" | php
RUN mv composer.phar /usr/local/bin/composer

RUN mkdir -p /workspace
WORKDIR /workspace
