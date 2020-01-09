FROM ubuntu:16.04
MAINTAINER Hugh Pierce

ENV DEBIAN_FRONTEND=noninteractive
ENV mysql_root_pwd=p@ssw0rd

# Update system & install packages
RUN apt-get update && apt-get -y upgrade && apt-get install -y acl curl git nano vim wget nginx php7.0-fpm php7.0-cli php7.0-intl php7.0-xml php7.0-mysql php7.0-zip mysql-server

# Setup MySQL
RUN usermod -d /var/lib/mysql/ mysql && \
  service mysql start && mysqladmin -u root password $mysql_root_pwd && \
  service mysql stop

# Fix PHP TZ
RUN  sed -i -e "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" \
    -e "s/;date.timezone.*$/date.timezone = \"UTC\"/" \
    /etc/php/7.0/fpm/php.ini && \
 sed -i "s/;date.timezone.*$/date.timezone = \"UTC\"/" /etc/php/7.0/cli/php.ini

# Copy data
COPY site-default /etc/nginx/site-default

# Default MySQL 
RUN  cp -f /etc/nginx/site-default /etc/nginx/sites-available/default && \
  ln -sf /etc/nginx/sites-available/* /etc/nginx/sites-enabled/ 

# Set permissions
RUN  chown -R mysql /var/lib/mysql && \
  mkdir -p /var/log/mysql && chown -R mysql /var/log/mysql && \
  chown -R www-data /var/www && \
  mkdir -p /var/log/nginx && chown -R www-data /var/log/nginx

EXPOSE 80

# Start services
ENTRYPOINT service mysql start && \
  service php7.0-fpm start && \
  service nginx start && \
  /bin/bash

