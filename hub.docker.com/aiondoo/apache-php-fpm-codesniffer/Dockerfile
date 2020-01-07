FROM cloudposse/apache-php-fpm:latest

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
    apt-get -y install \
      vim \
      zip \
      iputils-ping \
      mysql-client \
      php-bz2 \
      php-mbstring \
      php-zip \
      php-gmp && \
      apt-get clean && \
      rm -f /var/www/html/index.html && \
      echo '<?php // sleep is good ?>' > /var/www/html/index.php

## Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

## Install codesniffer
RUN wget https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar
RUN chmod +x phpcs.phar
RUN mv phpcs.phar /usr/local/bin/phpcs

### Install PHPCompatibility
RUN mkdir -p /opt/src
RUN wget https://github.com/wimg/PHPCompatibility/archive/master.zip
RUN unzip master.zip
RUN mv PHPCompatibility-master/ /opt/src
RUN phpcs --config-set installed_paths /opt/src/PHPCompatibility-master/PHPCompatibility
RUN rm master.zip

## Install mess detector
RUN wget http://static.phpmd.org/php/latest/phpmd.phar
RUN chmod +x phpmd.phar
RUN mv phpmd.phar /usr/local/bin/phpmd
