FROM ubuntu:latest

# Install apache, PHP, and supplimentary programs. openssh-server, curl, and lynx-cur are for debugging the container.
RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apache2 php7.0 php7.0-mysql libapache2-mod-php7.0 curl git php7.0-xml unzip mysql-client phpunit php7.0-mbstring npm

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite

# Update apache php.ini file
ADD php/php.ini /etc/php/7.0/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

# Copy this repo into place
RUN mkdir -p /var/www/espeo-api
RUN mkdir -p /var/www/espeo-front

# Git
RUN git clone --progress https://negass@bitbucket.org/negass/espeo.git  /var/www/espeo-api/
RUN cd /var/www/espeo-api && composer install --no-interaction

RUN git clone --progress https://negass@bitbucket.org/negass/espeo-front.git  /var/www/espeo-front/
RUN cd /var/www/espeo-front && npm install && npm install gulp

# Prepare permissions
RUN usermod -u 1000 www-data
RUN chmod -R 775 /var/www/espeo-api/*
RUN chown -R www-data:www-data /var/www/espeo-api/*

RUN chmod -R 775 /var/www/espeo-front/*
RUN chown -R www-data:www-data /var/www/espeo-front/*

# Remove unnecessary default vhost
RUN rm /etc/apache2/sites-available/000-default.conf
RUN rm /etc/apache2/sites-enabled/000-default.conf

# Update the default apache site with the config we created.
COPY apache/espeo-api.conf /etc/apache2/sites-available/
COPY apache/espeo-front.conf /etc/apache2/sites-available/
RUN a2ensite espeo-api.conf
RUN a2ensite espeo-front.conf

CMD /usr/sbin/apache2ctl -D FOREGROUND