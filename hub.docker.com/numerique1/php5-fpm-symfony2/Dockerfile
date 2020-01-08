FROM php:5.6-fpm

RUN echo "date.timezone = Europe/Paris" >> /usr/local/etc/php/php.ini

RUN apt-get update -qq
RUN apt-get -qqy install php5-mysql

RUN echo "extension=/usr/lib/php5/20131226/pdo.so" >> /usr/local/etc/php/php.ini
RUN echo "extension=/usr/lib/php5/20131226/pdo_mysql.so" >> /usr/local/etc/php/php.ini

RUN echo "memory_limit = 512M" >> /usr/local/etc/php/php.ini


