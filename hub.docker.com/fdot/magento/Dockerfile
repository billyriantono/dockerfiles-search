FROM ubuntu:14.04


#=============#
# Information #
#=============#
# Based on: Ubuntu 14.04 (Trusty)
# Docker Hub: https://hub.docker.com/_/ubuntu/
# Github: https://github.com/tianon/docker-brew-ubuntu-core/tree/9c78896fe39d5be95cc4a6ae6c0475599a1bc396/trusty


#===========================#
# Basics and PHP Extensions #
#===========================#
ENV DEBIAN_FRONTEND noninteractive
ENV PKGS_BASICS='tar vim'
ENV PKGS_PHP='php5 php5-cli php5-mysql php5-curl php5-gd php5-mcrypt php5-common php-xml-parser unzip'
RUN \
  apt-get update -y -qq && \
  apt-get dist-upgrade -y -qq && \
  apt-get install -y -qq $PKGS_BASICS $PKGS_PHP && \
  php5enmod mcrypt


#=======#
# MySQL #
#=======#
ENV DB_SERVER 127.0.0.1
ENV DB_PORT 3306
ENV DB_NAME magento
ENV DB_USER magento
ENV DB_PASSWD magento
ENV DB_ROOT_USER root
ENV DB_ROOT_PASSWD admin
ENV PKGS_MYSQL='mysql-server mysql-client'
RUN echo mysql-server-5.6 mysql-server/root_password password $DB_ROOT_PASSWD | debconf-set-selections && \
  echo mysql-server-5.6 mysql-server/root_password_again password $DB_ROOT_PASSWD | debconf-set-selections && \
  apt-get install -y -qq $PKGS_MYSQL
# MySQL configuration
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf
VOLUME /var/log/apache2/
EXPOSE 3306


#========#
# Apache #
#========#
COPY resources/config_files/apache2.conf /etc/apache2/
COPY resources/config_files/magento /etc/sudoers.d
COPY resources/scripts/apache2-foreground /usr/local/bin
RUN chmod +x /usr/local/bin/apache2-foreground && \
  a2enmod rewrite && \
  groupadd -g 10000 magento && \
  useradd -p magento magento -u 10000 -g 10000
WORKDIR /var/www/html
EXPOSE 80


#============================#
# Magento (Main Application) #
#============================#
# Main Application
ENV MAGENTO_VERSION 1.9.3.2
ARG SITE_IP
ENV DOMAIN ${DOMAIN}
ENV SITE_URL "http://192.168.99.100"
ENV ADMIN_USERNAME "magento"
ENV ADMIN_PASSWORD "azerty1234"
ENV ADMIN_FIRSTNAME "magento"
ENV ADMIN_LASTNAME "magento"
ENV ADMIN_EMAIL "test@example.com"
ENV LOCALE "fr_FR"
ENV TIMEZONE "Europe/Paris"
ENV DEFAULT_CURRENCY "EUR"
ENV USE_SECURE "no"
ENV SECURE_BASE_URL "http://192.168.99.100"
ENV URL_REWRITE "yes"
ENV SKIP_URL_VALIDATION "yes"
ENV USE_SECURE_ADMIN "no"
COPY resources/magento-$MAGENTO_VERSION.tar.gz /tmp
USER magento
RUN cd /tmp; \
  sudo chown -R magento:magento /var/www; \
  tar -zxf magento-$MAGENTO_VERSION.tar.gz; \
  rm -rf /var/www/html; \
  mv /tmp/magento /tmp/html; \
  mv /tmp/html /var/www; \
  sudo rm -f /tmp/magento-$MAGENTO_VERSION.tar.gz && \
  mkdir -p /var/www/html/var/log /var/www/html/var/report
VOLUME /var/www/html/var/log
VOLUME /var/www/html/var/report


#=======================#
# Magento (Sample Data) #
#=======================#
# NB: tar -zxf /tmp/magento-sample-data-$DATA_VERSION.tar.gz won't work
# Need to unzip and untar separately
# Don't know why ...
# ENV DATA_VERSION 1.9.2.4
# ENV INSTALL_SAMPLE_DATA 0
# COPY resources/magento-sample-data-$DATA_VERSION.tar.gz /tmp
# RUN cd /tmp; \
#  gunzip magento-sample-data-$DATA_VERSION.tar.gz; \
#  tar xf magento-sample-data-$DATA_VERSION.tar; \
#  mv magento-sample-data-$DATA_VERSION magento-sample-data && \
#  mv /tmp/magento-sample-data/magento_sample_data_for_$DATA_VERSION.sql /tmp/magento_sample_data.sql && \
#  mv -f /tmp/magento-sample-data/media /var/www/html/media && \
#  mv -f /tmp/magento-sample-data/skin /var/www/html/skin && \
#  rm -rf /tmp/magento-sample-data && \
#  rm -f /tmp/magento-sample-data-$SAMPLE_DATA_VERSION.tar.gz


#=======================#
# Magento (Custom Data) #
#=======================#
# Add "Products" and "Customers"
ENV DATA_VERSION 1.9.1.1
ENV INSTALL_CUSTOM_DATA 1
COPY resources/magento-custom-data-$DATA_VERSION.tar.gz /tmp
RUN cd /tmp; \
 tar -zxf magento-custom-data-$DATA_VERSION.tar.gz; \
 mv magento-custom-data-$DATA_VERSION magento-custom-data && \
 mv /tmp/magento-custom-data/magento_custom_data.sql /tmp/magento_custom_data.sql && \
 rm -rf /var/www/html/media/* && \
 mv /tmp/magento-custom-data/media/* /var/www/html/media && \
 sudo rm -rf /tmp/magento-custom-data && \
 sudo rm -f /tmp/magento-custom-data-$SAMPLE_DATA_VERSION.tar.gz


#==============#
# Installation #
#==============#
COPY resources/scripts /scripts
RUN sudo chown -R magento:magento /scripts && \
  sudo chmod -R +x /scripts && \
  sudo chown -R magento:magento /var/www/html && \
  sudo chown -R magento:magento /tmp/*
RUN bash /scripts/install_magento.sh && \
  sudo rm -rf /tmp/*

#=============#
# Here we go! #
#=============#
CMD ["/scripts/run.sh"]