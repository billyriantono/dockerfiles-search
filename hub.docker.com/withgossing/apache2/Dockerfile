FROM ubuntu:16.04
MAINTAINER Seungyoun Ko <withgossing@gmail.com>

ENV APACHE_RUN_USER   www-data
ENV APACHE_RUN_GROUP  www-data
ENV APACHE_PID_FILE   /var/run/apache2.pid
ENV APACHE_RUN_DIR    /var/run/apache2
ENV APACHE_LOCK_DIR   /var/lock/apache2
ENV APACHE_LOG_DIR    /var/log/apache2
ENV APACHE_USER_UID   0

# apt-get
RUN apt-get update && apt-get -y upgrade

# apache2
RUN apt-get install -y apache2
RUN a2enmod rewrite
RUN a2enmod headers
RUN a2dismod -f autoindex
RUN echo 'ServerName localhost:80' >> /etc/apache2/apache2.conf

# php7
RUN apt-get install -y php libapache2-mod-php7.0 php-mcrypt php-mbstring php-gd php-curl
RUN echo '<?php phpinfo(); ?>' >> /var/www/html/index.php

VOLUME ["/var/www/html"]

CMD ["/usr/sbin/apache2", "-DFOREGROUND"]

EXPOSE 80
