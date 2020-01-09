FROM php:5.6-apache

COPY lam/lam /var/www/html/

RUN apt-get update && apt-get install -y \
        gettext \
        zlib1g-dev

RUN docker-php-ext-install zip

RUN \
    apt-get update && \
    apt-get install libldap2-dev -y && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap

RUN docker-php-ext-install gettext

RUN mkdir -p /var/www/html/sess
RUN mkdir -p /var/www/html/tmp
RUN chown www-data:www-data /var/www/html/sess
RUN chown www-data:www-data /var/www/html/tmp
RUN chmod 755 /var/www/html/sess
RUN chmod 755 /var/www/html/tmp
