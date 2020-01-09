FROM php:7.1-apache
MAINTAINER Markus Klinger <klinger@pierraa-group.de>

# Here we could config the php ini to work with Flow
#COPY config/php.ini /usr/local/etc/php/

# We need Git to use composer
RUN apt-get update &&\
    apt-get install --yes --no-install-recommends git-all zip unzip

# Install composer
RUN curl -s https://getcomposer.org/installer | php

RUN cd /var/www/html/ && \
    php composer.phar create-project --keep-vcs neos/flow-base-distribution tutorial 3.0.0
RUN ls

VOLUME /var/www/html/
