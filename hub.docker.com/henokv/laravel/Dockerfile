FROM php:7.1
MAINTAINER ISW Leuven <support@iswleuven.be>
RUN apt-get update -yqq \
  && apt-get install -y gnupg2 \
  && curl -sL https://deb.nodesource.com/setup_7.x | bash - \
  && apt-get install git gnupg2 nodejs libcurl4-gnutls-dev libicu-dev libmcrypt-dev libvpx-dev libjpeg-dev libpng-dev libxpm-dev libldap2-dev libxml2-dev libbz2-dev -y && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \
  && docker-php-ext-install mbstring mcrypt pdo_mysql curl json intl gd xml zip bz2 opcache ldap \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug
