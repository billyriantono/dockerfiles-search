FROM php:7.0-apache
LABEL maintainer="maximilianschmidt404@gmail.com"

RUN apt-get update -y && \
apt-get upgrade -y --with-new-pkgs && \
apt-get autoremove -y

RUN apt-get update -y && \
apt-get install -y git wget zip unzip libzip-dev libmcrypt-dev libpq-dev libcurl4-gnutls-dev libicu-dev libvpx-dev libjpeg-dev libpng-dev libxpm-dev zlib1g-dev libfreetype6-dev libxml2-dev libexpat1-dev libbz2-dev libgmp3-dev libldap2-dev unixodbc-dev libsqlite3-dev libaspell-dev libsnmp-dev libpcre3-dev libtidy-dev

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
php composer-setup.php --install-dir=/usr/local/bin --filename=composer && rm composer-setup.php

RUN curl --location --output /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar && \
chmod +x /usr/local/bin/phpunit

RUN php -r "exit((int)(extension_loaded('mbstring')==false));" || docker-php-ext-install mbstring
RUN php -r "exit((int)(extension_loaded('mcrypt')==false));" || docker-php-ext-install mcrypt
RUN php -r "exit((int)(extension_loaded('tokenizer')==false));" || docker-php-ext-install tokenizer
RUN php -r "exit((int)(extension_loaded('pdo_mysql')==false));" || docker-php-ext-install pdo_mysql
RUN php -r "exit((int)(extension_loaded('pdo_pgsql')==false));" || docker-php-ext-install pdo_pgsql
RUN php -r "exit((int)(extension_loaded('curl')==false));" || docker-php-ext-install curl
RUN php -r "exit((int)(extension_loaded('json')==false));" || docker-php-ext-install json
RUN php -r "exit((int)(extension_loaded('intl')==false));" || docker-php-ext-install intl
RUN php -r "exit((int)(extension_loaded('gd')==false));" || docker-php-ext-install gd
RUN php -r "exit((int)(extension_loaded('json')==false));" || docker-php-ext-install json
RUN php -r "exit((int)(extension_loaded('xml')==false));" || docker-php-ext-install xml
RUN php -r "exit((int)(extension_loaded('bz2')==false));" || docker-php-ext-install bz2
RUN php -r "exit((int)(extension_loaded('opcache')==false));" || docker-php-ext-install opcache

RUN php -r "exit((int)(extension_loaded('zip')==false));" || \
docker-php-ext-configure zip --with-libzip && \
docker-php-ext-install zip

RUN pecl install xdebug && docker-php-ext-enable xdebug