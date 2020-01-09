# This is a PlexityNet docker container for Drupal 8.

FROM plexitynet/base14:latest
MAINTAINER Saul Willers <saul@plexitynet.com>

ENV REFRESHED_AT 2018-03-06

### APT.

RUN apt-get update
RUN apt-get -y upgrade

### Apache.

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apache2 \
    php5 \
    libapache2-mod-php5 \
    php5-curl \
    php5-mysql \
    php5-gd \
    php5-mcrypt \
    php-pear \
    php5-dev \
    nullmailer \
    build-essential

ADD ./scripts/foreground.sh /etc/apache2/foreground.sh
RUN chmod 755 /etc/apache2/foreground.sh
RUN rm -rf /var/www/
RUN mkdir /var/www
RUN mkdir /var/www/current
RUN mkdir /var/www/current/app
RUN chown -R www-data:www-data /var/www

# Mods.

RUN cd /etc/apache2/mods-enabled && ln -s ../mods-available/rewrite.load .
RUN cd /etc/apache2/mods-enabled && ln -s ../mods-available/headers.load .

# vHost.

RUN rm -f /etc/apache2/sites-enabled/*
ADD ./conf/apache2/drupal.conf /etc/apache2/drupal.conf
ADD ./conf/apache2/default.conf /etc/apache2/sites-available/default.conf
RUN ln -s /etc/apache2/sites-available/default.conf /etc/apache2/sites-enabled/default.conf

### PHP.

ADD ./conf/php/php.ini /etc/php5/apache2/php.ini
ADD ./conf/php/php.ini /etc/php5/cli/php.ini
# PECL.
RUN pecl install uploadprogress
ADD ./conf/php/uploadprogress.ini /etc/php5/conf.d/uploadprogress.ini

# Drush.
ADD https://github.com/drush-ops/drush/archive/6.7.0.zip /tmp/drush.zip
RUN cd /tmp && unzip /tmp/drush.zip
RUN mv /tmp/drush-6.7.0 /opt/drush
RUN ln -s /opt/drush/drush /usr/local/bin/drush
RUN chmod -R 777 /opt/drush/lib
# Run drush once, so Console_Table is downloaded and installed.
RUN /usr/local/bin/drush

### Mysql.

# This container is a simple client designed to connect (i.e. linked in docker)
# to another container running a mysql server.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mysql-client

### Supervisord.

# Append our new conf to existing conf from base image.
ADD ./conf/supervisor/supervisord.conf /etc/supervisord.2.conf
RUN cat /etc/supervisord.2.conf >> /etc/supervisord.conf
RUN rm -f /etc/supervisord.2.conf

### Startup scripts.

ADD ./scripts/start.sh /root/start.sh
RUN chmod 755 /root/start.sh

EXPOSE 80

CMD ["/root/start.sh"]
