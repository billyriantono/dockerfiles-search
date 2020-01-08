# airchen233/gproject

FROM php:5.6.34-fpm

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN mkdir -p /work

WORKDIR /work

RUN apt-get update && apt-get install -y libssl-dev && pecl install mongo

EXPOSE 9000