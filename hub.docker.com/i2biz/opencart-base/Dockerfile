FROM php:7.2.6-apache-stretch

COPY setup-system.sh /opt/setup-system.sh
COPY php.ini /usr/local/etc/php
RUN /opt/setup-system.sh

VOLUME /var/www/html/
VOLUME /var/www/html/system/storage/
VOLUME /var/www/html/image/
