FROM ubuntu:latest
MAINTAINER Raphael Zimmermann <mister.norbert@gmail.com>

# Update
RUN apt-get update

# Install base PHP
RUN apt-get install -yqq apache2 libapache2-mod-php5

# Install curl
RUN apt-get install -yqq curl

# Install specific dependencies
RUN apt-get install -yqq php5-gd php5-json php5-curl
RUN apt-get install -yqq php5-intl php5-mcrypt php5-imagick php5-mysql

ADD ./001-app.conf /etc/apache2/sites-available/
RUN ln -s /etc/apache2/sites-available/001-app.conf /etc/apache2/sites-enabled/
RUN a2enmod rewrite

ADD php.ini /etc/php5/apache2/php.ini

# Change uuid of user to 1000 - for easy development...
RUN usermod -u 1000 www-data

# Run apache
CMD apache2ctl -DFOREGROUND

# Expose HTTP and HTTPS ports
EXPOSE 80 443

# Workdir shall be the webserver root
WORKDIR /var/www/html

# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php
RUN mv composer.phar /usr/local/bin/composer

# Install git (for drone builds...)
RUN apt-get install -yqq git
