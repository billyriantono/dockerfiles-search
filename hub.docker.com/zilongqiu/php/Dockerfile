FROM php:7-fpm
MAINTAINER Zi-long QIU <zilong.qiu@gmail.com>

COPY ./configs/php.ini /usr/local/etc/php/php.ini
RUN sed -i 's/;date.timezone =/date.timezone = "Europe\/Paris"/g' /usr/local/etc/php/php.ini