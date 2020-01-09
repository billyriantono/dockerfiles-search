#
# Dockerfile for maintenance-page
#

FROM php:7-apache
MAINTAINER aaron <info@aamservices.uk>

RUN a2enmod rewrite headers

WORKDIR /var/www/html

COPY .htaccess .htaccess
COPY maintenance.php maintenance.php

EXPOSE 80
