FROM php:7.1-cli

MAINTAINER Thomas L. Johnsen

RUN apt-get -y update \
&& apt-get -y install git unzip curl zlib1g-dev

RUN docker-php-ext-install mysqli pdo pdo_mysql zip

RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN apt-get autoremove -y \
&& apt-get clean all
