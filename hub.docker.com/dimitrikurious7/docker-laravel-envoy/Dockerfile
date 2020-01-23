FROM php:latest
MAINTAINER Dimitri <dimitri@kurious7.be>

RUN apt-get update
RUN apt-get install -y unzip libmcrypt-dev openssh-client
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require laravel/envoy
