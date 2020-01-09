FROM php:7.3-apache

RUN apt-get update && \
 apt-get install --yes --force-yes cron g++ gettext libicu-dev openssl libc-client-dev \
 libkrb5-dev  libxml2-dev libfreetype6-dev libgd-dev libmcrypt-dev bzip2 libbz2-dev \
 libtidy-dev libcurl4-openssl-dev libz-dev libmemcached-dev libxslt-dev  && \
# PHP Configuration
 docker-php-ext-install bcmath && \
 docker-php-ext-install bz2 && \
 docker-php-ext-install calendar && \
 docker-php-ext-install dba && \
 docker-php-ext-install exif && \
 docker-php-ext-install fileinfo && \
 docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr && \
 docker-php-ext-install gd && \
 docker-php-ext-install gettext && \
 docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
 docker-php-ext-install imap && \
 docker-php-ext-install intl && \
 docker-php-ext-install pdo pdo_mysql && \
 docker-php-ext-install soap && \
 docker-php-ext-install tidy && \
 docker-php-ext-install xmlrpc && \
 docker-php-ext-install mbstring  && \
 docker-php-ext-install xsl  && \
 docker-php-ext-install mysqli  && \
 docker-php-ext-configure zip --enable-zip --without-libzip  && \
 docker-php-ext-install zip  && \
 docker-php-ext-configure hash --with-mhash  && \
# Apache Configuration
 a2enmod rewrite  && \
 a2enmod headers  && \
 a2enmod deflate  && \
# SSL
 a2enmod ssl  && \
 a2ensite default-ssl  && \
 openssl req -subj '/CN=example.com/O=My Company Name LTD./C=US' -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout /etc/ssl/private/ssl-cert-snakeoil.key -out /etc/ssl/certs/ssl-cert-snakeoil.pem  && \
# Imagemagick
 apt-get install --yes --force-yes libmagickwand-dev libmagickcore-dev  && \
 yes '' | pecl install -f imagick  && \
 docker-php-ext-enable imagick

