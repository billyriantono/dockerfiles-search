FROM php:7-apache

WORKDIR /var/www

RUN echo "deb http://mirrors.163.com/debian/ jessie main non-free contrib" > /etc/apt/sources.list \
  && echo "deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib" >> /etc/apt/sources.list \
  && echo "deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib" >> /etc/apt/sources.list \
  && apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        wget \
        unzip\
  && docker-php-ext-install -j$(nproc) iconv mcrypt \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install -j$(nproc) gd \
  && wget https://builds.piwik.org/piwik.zip \
  && unzip piwik.zip \
  && mv piwik/* /var/www/html/ \
  && chmod -R 777 /var/www/html \
  && rm -Rf /var/www/html/plugins/Morpheus/icons/submodules \
  && apt-get remove -y wget unzip \
  && apt-get autoremove -y \
  && apt-get clean autoclean 

WORKDIR /var/www/html
