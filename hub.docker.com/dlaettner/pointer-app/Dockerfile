FROM php:7.2-apache

COPY ./classes /var/www/html/classes
COPY ./resources /var/www/html/resources
COPY ./sql /var/www/html/sql
COPY ./*.php /var/www/html/

RUN docker-php-ext-install mysqli
# && docker-php-ext-enable mysqli
