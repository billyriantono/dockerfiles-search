FROM ubuntu:18.04

MAINTAINER Alizadeh Mammadali

RUN apt-get update
# RUN apt-get -y upgrade

# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 git apt-utils libapache2-mod-php php-pear php-fpm php-dev php-zip php-curl php-xmlrpc php-gd php-mysql php-mbstring php-xml php-gd php-zip php-curl php-tidy

RUN apt-get install -y vim nano

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

# Enable apache mods.

RUN a2enmod php7.2
RUN a2enmod rewrite
RUN service apache2 restart
RUN chgrp -R www-data /var/www/html
RUN find /var/www/html -type d -exec chmod g+rx {} +
RUN find /var/www/html -type f -exec chmod g+r {} +
RUN chown -R root /var/www/html/
RUN find /var/www/html -type d -exec chmod u+rwx {} +
RUN find /var/www/html -type f -exec chmod u+rw {} +
RUN find /var/www/html -type d -exec chmod g+s {} +

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80


# By default, simply start apache.
CMD /usr/sbin/apache2ctl -D FOREGROUND
