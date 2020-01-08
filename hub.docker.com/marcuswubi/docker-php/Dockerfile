FROM marcuswubi/docker-apache:16.04

MAINTAINER maviniciuus <maviniciuus@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
apt-get install -y php7.0 \
libapache2-mod-php7.0 \
php7.0-xml \
php7.0-xmlrpc \
php7.0-fpm \
php7.0-cli \
php7.0-curl \
php7.0-gd \
php7.0-mcrypt \
php-apcu \
php7.0-json \
php7.0-pgsql \
php7.0-mysql \
php7.0-zip \
php7.0-mbstring \
php7.0-soap && \

phpenmod mcrypt && \
rm -rf /var/lib/apt/lists/*
