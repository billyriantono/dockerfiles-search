FROM ubuntu:xenial

#
# installs nextcloud
#

USER root

ENV INSTALL_FILE nextcloud-13.0.6.tar.bz2
ENV NXT_SHA256 90fc9e960b6a477bb14ee87042b3d158bde95c3f0157677cb4547ca7649968d4
ENV INSTALL_DIR /var/www
ENV VOLUME_DIR /var/owncloud_volume

RUN DEBIAN_FRONTENT=noninteractive apt-get update && apt-get install -yq apt-utils

RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq bzip2 apache2 mariadb-server libapache2-mod-php7.0 php7.0-gd php7.0-json php7.0-mysql php7.0-curl php7.0-intl php7.0-mcrypt php-imagick php-oauth php7.0-xml php7.0-zip php7.0-mbstring php7.0-sqlite3 patch sudo exim4-daemon-light

# remove the password of debians mysql maintenance user
RUN sed -i 's/password = .*$/password = /g' /etc/mysql/debian.cnf 

# download and verify nextcloud, and extract to $INSTALL_DIR/nextcloud
RUN rm -rf $INSTALL_DIR/*
ADD https://download.nextcloud.com/server/releases/$INSTALL_FILE $INSTALL_DIR/$INSTALL_FILE
#RUN cd $INSTALL_DIR/ && sha256sum -c ${INSTALL_FILE}.sha256
RUN cd $INSTALL_DIR && echo $NXT_SHA256 ${INSTALL_FILE} | sha256sum -c - 
RUN cd $INSTALL_DIR && tar xjf $INSTALL_FILE
RUN rm $INSTALL_DIR/$INSTALL_FILE
RUN mkdir $INSTALL_DIR/nextcloud/data

# default to read access for www-data (except apps and config dirs)
RUN chown -R root:root $INSTALL_DIR && find $INSTALL_DIR -type d -exec chmod 755 {} \; && find $INSTALL_DIR -type f -exec chmod 644 {} \;
RUN chown -R www-data:www-data $INSTALL_DIR/nextcloud/apps/
RUN chown www-data:www-data $INSTALL_DIR/nextcloud/config/
RUN chown www-data:www-data $INSTALL_DIR/nextcloud/data/
RUN touch $INSTALL_DIR/index.html

# link nextcloud/config/config.php to our volume/config/config.php
RUN mkdir -p $VOLUME_DIR/config && mkdir -p $VOLUME_DIR/data
RUN touch $VOLUME_DIR/config/config.php && ln -s $VOLUME_DIR/config/config.php $INSTALL_DIR/nextcloud/config/config.php

# some php settings
RUN sed -i 's/^max_input_time = .*$/max_input_time = 500/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/^max_execution_time = .*$/max_execution_time = 500/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/^memory_limit = .*$/memory_limit = 1024M/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/^post_max_size = .*$/post_max_size = 50M/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/^upload_max_filesize = .*$/upload_max_filesize = 1024M/' /etc/php/7.0/apache2/php.ini

# disable all apache config except ours
ADD conf/apache.conf /etc/apache2/sites-available/nextcloud.conf
RUN a2dissite "*"
RUN a2ensite nextcloud
RUN a2enmod rewrite
RUN a2dismod status

# enable MySQL 4Byte Support and PHP opcache
ADD conf/99-nextcloud-4byte-support.cnf /etc/mysql/mariadb.conf.d/
ADD conf/99-opcache.ini /etc/php/7.0/apache2/conf.d/99-opcache.ini

VOLUME ["/var/lib/mysql", "/var/owncloud_volume"]

EXPOSE 80

ADD startup.sh /
RUN chmod +x /startup.sh
CMD ["/startup.sh"]
