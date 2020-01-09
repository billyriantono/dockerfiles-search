FROM php:5.6-apache

ENV ENVIRONMENT production

RUN echo "[PHP] \ndate.timezone = Asia/Bangkok" >> /usr/local/etc/php/php.ini

RUN apt-get -y update \
    && apt-get install -y --no-install-recommends \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-install mysqli

RUN a2enmod 
RUN rewrite

COPY ./index.php /var/www/html/index.php
VOLUME [ "/var/www/html" ]

EXPOSE 80 443
