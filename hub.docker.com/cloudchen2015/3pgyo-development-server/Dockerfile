FROM php:5.6-apache
MAINTAINER CloudChen<cloudchen2015@gmail.com>

RUN \
    docker-php-ext-install mysql mysqli pdo_mysql

RUN \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
    -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
    -subj "/C=TW/ST=Taiwan/L=Taipei/O=BlackHand/OU=Development/CN=blackhand"

RUN \
    a2enmod rewrite && \
    a2ensite default-ssl && \
    a2enmod ssl

COPY ./docker/php.ini /usr/local/etc/php/

EXPOSE 80 443
