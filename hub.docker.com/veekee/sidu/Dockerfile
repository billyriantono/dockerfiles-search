# SIDU DB Web GUI
# http://topnew.net/sidu/

# Added parts from https://github.com/wdekkers/docker-php7-httpd-apache2-mysql

FROM php:7-apache

MAINTAINER VeekeeFr

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev apt-utils wget curl vim zip unzip

RUN apt-get install -y \
        libxml2-dev libzip-dev

RUN /usr/local/bin/docker-php-ext-install mysqli pdo pdo_mysql zip xmlwriter
RUN apt-get install libssl-dev -y

RUN /usr/local/bin/docker-php-ext-install zip

# Install mcrypt
RUN apt-get install -y libmcrypt-dev
RUN pecl install mcrypt-1.0.2
RUN docker-php-ext-enable mcrypt

# Install GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

# Install XSL
RUN apt-get install -y libxslt-dev
RUN docker-php-ext-install xsl

RUN a2enmod rewrite
RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

# Export name-version-release.
ENV SIDU_VERSION sidu61

# Install
ADD ${SIDU_VERSION}.md5sum /tmp/
RUN cd /tmp/ && \
    wget http://downloads.sourceforge.net/sidu/${SIDU_VERSION}.zip && \
    md5sum -c ${SIDU_VERSION}.md5sum && \
    mkdir -p /var/www/html && \
    unzip ${SIDU_VERSION}.zip && \
    mv ${SIDU_VERSION}/* /var/www/html && \
    rm -fr /tmp/*
