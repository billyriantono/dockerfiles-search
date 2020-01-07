FROM php:7-apache

LABEL maintainer="Irvin Capagcuan"

RUN a2enmod rewrite

COPY 000-default.conf /etc/apache2/sites-available/

ENV APP_ENV=prod
