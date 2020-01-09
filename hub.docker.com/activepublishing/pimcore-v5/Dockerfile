FROM php:7.1.18-apache

########################################################################################################################
## ENV
########################################################################################################################

ENV APT_INSTALL_CMD 'apt-get -qq install -y --no-install-recommends -qq'
ENV HOME_AP /usr/actpub
ENV PIMCORE_ROOT /home/www/pimcore_root
ENV PIMCORE_VAR /home/www/pimcore_var
ENV PIMCORE_BUNDLE_ROOT $PIMCORE_ROOT/src
ENV APACHE_DOCUMENT_ROOT $PIMCORE_ROOT/web
ENV PHP_DEBUG 0

########################################################################################################################
## SYSTEM
########################################################################################################################

## Add backports support
RUN apt-get update && \
    $APT_INSTALL_CMD lsb-release apt-utils > /dev/null && \
    echo "deb http://deb.debian.org/debian $(lsb_release -sc)-backports main" > /etc/apt/sources.list.d/backports.list && \
    apt-get -qq update > /dev/null

## Enable Apache rewrite mod
RUN a2enmod rewrite

## Required Settings, Modules & Extensions for Pimcore 5.2.x
RUN APT_DEPS="libxml2-dev libxslt1.1 libxslt1-dev libxml2-dev libpng-dev zlib1g-dev libbz2-dev libicu-dev" && \
    APT_DEPS="${APT_DEPS} libmagickwand-dev libc-client-dev libkrb5-dev wget mysql-client" && \
    APT_DEPS="${APT_DEPS} ffmpeg ghostscript xvfb html2text coreutils poppler-utils inkscape libimage-exiftool-perl" && \
    APT_DEPS="${APT_DEPS} libreoffice libreoffice-script-provider-python libreoffice-math xfonts-75dpi poppler-utils" && \
    APT_DEPS="${APT_DEPS} inkscape libxrender1 libfontconfig1 pdftk unzip git net-tools cron nano" && \
    $APT_INSTALL_CMD $APT_DEPS > /dev/null

RUN PHP_PKGS="pdo_mysql mysqli iconv dom simplexml gd exif fileinfo mbstring zip bz2 intl opcache soap" && \
    docker-php-ext-install $PHP_PKGS > /dev/null && \
    docker-php-ext-enable $PHP_PKGS

RUN PECL_PKGS="imagick redis" && \
    PHP_PKGS="imap" && \
    docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
    pecl install $PECL_PKGS > /dev/null && \
    docker-php-ext-install $PHP_PKGS > /dev/null && \
    docker-php-ext-enable $PECL_PKGS $PHP_PKGS

RUN $APT_INSTALL_CMD locales-all > /dev/null

## Add bin additional software
COPY resources/bin/ /usr/local/bin/
RUN chmod -R 755 /usr/local/bin/

## Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN chmod -R 755 /usr/local/bin/
RUN mkdir /var/www/.composer && chmod -R 0777 /var/www/.composer

## Install wkhtmltox
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb && \
      $APT_INSTALL_CMD -f xfonts-base && \
      dpkg -i wkhtmltox_0.12.5-1.stretch_amd64.deb && \
      rm -rf wkhtmltox_0.12.5-1.stretch_amd64.deb

########################################################################################################################
## CONFIG
########################################################################################################################

## EXPOSE 8080
RUN sed -ri -e 's!80!8080!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!80!8080!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN sed -ri -e 's!Listen 80!Listen 8080!g' /etc/apache2/ports.conf

EXPOSE 8080

## RUN as www-data
RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

RUN chown -R www-data:www-data /var/lock/apache2
RUN chown -R www-data:www-data /var/run/apache2

# Change directory web
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# COPY PHP.ini
COPY resources/config/php.ini /usr/local/etc/php/php.ini

# COPY CRON
COPY resources/config/crontab /usr/crontab
RUN chmod 0644 /usr/crontab
RUN chmod +x /usr/local/bin/go-crond

# Create AP Dir
RUN mkdir -p $HOME_AP
RUN chown www-data:www-data $HOME_AP

########################################################################################################################
## Create base dir for PIMCORE and add file configuration
########################################################################################################################

RUN mkdir -p $PIMCORE_ROOT
RUN mkdir -p $PIMCORE_VAR/cache/pimcore
RUN mkdir -p $PIMCORE_VAR/cache/symfony
RUN mkdir -p $PIMCORE_VAR/logs
RUN mkdir -p $PIMCORE_VAR/email
RUN mkdir -p $PIMCORE_VAR/tmp_system
RUN mkdir -p $PIMCORE_VAR/tmp_web
RUN mkdir -p $HOME_AP/pimcore

ADD resources/config/pimcore/constants.php $HOME_AP/pimcore/constants.php

RUN chown -R www-data:www-data $PIMCORE_ROOT
RUN chown -R www-data:www-data $PIMCORE_VAR
RUN chown -R www-data:www-data $HOME_AP

WORKDIR $PIMCORE_ROOT

########################################################################################################################
# ENTRYPOINT
########################################################################################################################

COPY resources/scripts/entrypoint.sh /usr/local/bin
RUN chown www-data:www-data /usr/local/bin/entrypoint.sh && chmod +x /usr/local/bin/entrypoint.sh

########################################################################################################################
# Starting
########################################################################################################################
USER 1000

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["apache2-foreground"]
