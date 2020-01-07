FROM ubuntu:trusty
MAINTAINER Nathan Henderson <nhenderson@ipg.com>
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y upgrade

# Keep upstart from complaining, Otherwise you cannot add repositories
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

RUN apt-get install -y wget nano vim

# Add HHVM repository
RUN wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
RUN echo deb http://dl.hhvm.com/ubuntu trusty main | sudo tee /etc/apt/sources.list.d/hhvm.list

# Run after setting repositories
RUN apt-get update -y

# Basic Requirements - Installing Nginx before HHVM allowed HHVM to detect Nginx and create the /etc/nginx/hhvm.conf file for you.
RUN apt-get -y install nginx hhvm curl git unzip supervisor
#We need to add a config file for supervisor, so stop the service that was auto-started on intstall
RUN service supervisor stop

# nginx config
RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf
RUN sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

RUN mkdir /var/www
RUN chown -R www-data:www-data /var/www

# Phpinfo for testing purposes, with hiphop it will only show text: Hiphop
RUN echo "<?php phpinfo(); ?>" > /var/www/phpinfo.php

# For newer NGINX
ADD ./nginx-site.conf /etc/nginx/sites-enabled/default
ADD ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN mkdir -p /etc/hhvm
ADD ./config.hdf /var/www/config.hdf

# Initialization and Startup Script
ADD ./start.sh /start.sh
RUN chmod 755 /start.sh

# private expose
EXPOSE 80

CMD ["/bin/bash", "/start.sh"]
