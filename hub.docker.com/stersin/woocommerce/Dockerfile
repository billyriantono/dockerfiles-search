FROM wordpress:4.8-apache

RUN apt-get update -qq && apt-get install -yqq libxml2-dev
RUN docker-php-ext-install soap

