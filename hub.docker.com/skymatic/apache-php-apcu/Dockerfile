FROM php:7.2-apache
MAINTAINER Tobias Hagemann <tobias.hagemann@skymatic.de>

RUN pecl install apcu \
  && docker-php-ext-enable apcu
