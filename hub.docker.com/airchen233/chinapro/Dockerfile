# airchen233/chinapro

FROM php:7.1.6-fpm

RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN mkdir -p /work

WORKDIR /work

RUN apt-get update && apt-get install -y libpng-dev libjpeg-dev

RUN docker-php-ext-configure gd --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install mysqli gd

EXPOSE 9000