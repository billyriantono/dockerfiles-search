FROM php:7.0.11-fpm-alpine

MAINTAINER Arnel Labarda <aqlx86@gmail.com>

RUN docker-php-ext-install pdo pdo_mysql gd

EXPOSE 9000

CMD ["php-fpm"]