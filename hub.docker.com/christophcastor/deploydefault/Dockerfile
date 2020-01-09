FROM php:7.2.3-fpm

MAINTAINER Christoph Castor version: 0.1


RUN apt-get update -q && DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y --no-install-recommends vim curl debconf subversion git apt-transport-https apt-utils python python-pip \
    build-essential locales acl mailutils wget zip unzip \
    zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev supervisor\
    gnupg gnupg1 gnupg2
RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get install -y \
        libzip-dev \
        zip \
  && docker-php-ext-configure zip --with-libzip \
  && docker-php-ext-install zip
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd
# Install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && apt-get install -y nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -yq yarn
RUN php -r "copy('https://getcomposer.org/installer', 'setup.php');"
RUN php setup.php --install-dir=/usr/local/bin
RUN php -r "unlink('setup.php');"
RUN pip install setuptools
RUN pip install --upgrade pip awsebcli awscli


#ADD ./eb.sh /var/eb.sh
#RUN /bin/sh /var/eb.sh