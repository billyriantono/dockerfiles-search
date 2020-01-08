FROM php:5.6-fpm

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y\
  libcurl4-gnutls-dev\
  libicu-dev\
  libmcrypt-dev\
  libxml2-dev\
 --no-install-recommends &&\
 apt-get autoremove -y && apt-get clean -y &&\
 rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install -j$(nproc) json intl curl xml mcrypt pdo_mysql

RUN pecl install xdebug &&\
 docker-php-ext-enable xdebug

RUN mkdir /usr/src/php && cd /usr/src/php &&\
 tar -x --strip-components=1 -f /usr/src/php.tar.xz &&\
 mv php.ini-production /usr/local/etc/php/php.ini &&\
 rm -rf /usr/src/php

RUN sed -i 's/^\;\?short_open_tag\s\?=.*/short_open_tag = On/;\
 s/^\;\?display_errors\s\?=.*/display_errors = On/;\
 s/^\;\?date\.timezone\s\?=.*/date\.timezone = Europe\/London/;\
 s/^\;\?cgi\.fix_pathinfo\s\?=.*/cgi\.fix_pathinfo = 0/'\
 /usr/local/etc/php/php.ini

RUN sed -i 's/^\;\?pm\.max_children\s\?=.*/pm\.max_children = 20/'\
 /usr/local/etc/php-fpm.d/www.conf

EXPOSE 9000

CMD ["php-fpm"]
