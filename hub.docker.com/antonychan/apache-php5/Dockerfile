FROM ubuntu:14.04

# make sure apt is up to date
RUN apt-get update
RUN apt-get -y -qq install apache2 wget git git-core curl

# https://github.com/docker-library/php/blob/master/5.4/apache/Dockerfile
RUN rm -rf /var/www/html && mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html && chown -R www-data:www-data /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html

# Apache + PHP requires preforking Apache for best results
RUN a2dismod mpm_event && a2enmod mpm_prefork

RUN mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.dist && rm /etc/apache2/conf-enabled/* /etc/apache2/sites-enabled/*

COPY apache2.conf /etc/apache2/apache2.conf

RUN apt-get -y -qq install php5 libapache2-mod-php5 php5-mcrypt php5-mysql php5-curl

RUN curl -sS https://getcomposer.org/installer | php

RUN mv composer.phar /usr/local/bin/composer
