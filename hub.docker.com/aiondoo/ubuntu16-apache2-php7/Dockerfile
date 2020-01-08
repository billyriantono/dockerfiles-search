FROM ubuntu:16.04

MAINTAINER Aleksandra Hubert "ana@aiondoo.com"

# Set the locale
RUN apt-get clean && apt-get update
RUN apt-get install locales

## Update locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    apt-add-repository multiverse && \
    apt-get update && \
    apt-get install -y apache2 && \
    apt-get install -y \
      libapache2-mod-php7.0 \
      php7.0 \
      php7.0-curl \
      php7.0-cli \
      php7.0-common \
      php7.0-mbstring \
      php7.0-gd \
      php7.0-intl \
      php7.0-xml \
      php7.0-mysql \
      php7.0-mcrypt \
      php7.0-zip \
      php7.0-bz2 \
      php7.0-gmp && \
    apt-get -y install \
      curl \
      wget \
      lynx \
      dos2unix \
      locales \
      vim \
      iputils-ping \
      mysql-client && \
    apt-get clean && \
    cd /var/www/html && echo '<?php // sleep is good ?>' > index.php

## Start apache
CMD apachectl -D FOREGROUND

## Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
