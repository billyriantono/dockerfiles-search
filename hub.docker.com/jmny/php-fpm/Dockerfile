FROM php:5-fpm
MAINTAINER Louis PERRIER <louis@jmny.eu>


RUN apt-get update && docker-php-ext-install pdo_mysql

ENTRYPOINT ["php-fpm"]
