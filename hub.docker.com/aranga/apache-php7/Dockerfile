FROM ubuntu:16.04

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid


RUN apt-get update && apt-get -y upgrade &&  apt-get -y install \
        apache2 php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-fpm php7.0-gd php7.0-json php-memcached curl lynx-cur vim \
        && a2enmod php7.0 && a2enmod rewrite \
        && rm /var/www/html/* -rf \
        && rm -rf /var/lib/apt/lists/*
