# VERSION 0.0.2
FROM ubuntu:14.10

MAINTAINER Ulrich Nitsche "u.nitsche@gmail.com"

RUN apt-get update -y
RUN apt-get install -y apache2
RUN apt-get install -y libapache2-mod-php5
RUN apt-get install -y curl

ENV APACHE_RUN_USER   www-data
ENV APACHE_RUN_GROUP  www-data
ENV APACHE_DOCUMENTROOT /var/www
ENV APACHE_PID_FILE     /var/run/apache2.pid
ENV APACHE_RUN_DIR      /var/run/apache2
ENV APACHE_LOCK_DIR     /var/lock/apache2
ENV APACHE_LOG_DIR      /var/log/apache2

ONBUILD ADD ./var-www-contents/ /var/www/

RUN apt-get install -y php5
RUN apt-get install -y php5-common
RUN apt-get install -y php5-dev
RUN apt-get install -y php5-gd
RUN apt-get install -y php5-memcache
RUN apt-get install -y php5-mcrypt
RUN apt-get install -y php5-xsl
RUN apt-get install -y php5-cli
RUN apt-get install -y php5-curl
RUN apt-get install -y php5-mysql

RUN a2enmod php5

ADD ./config/php.ini /etc/php5/apache2/php.ini
ADD ./config/php.ini /etc/php5/cli/php.ini

ADD ./config/default_vhost /etc/apache2/sites-available/default_vhost.conf

RUN a2dissite 000-default
RUN a2ensite default_vhost


RUN /etc/init.d/apache2 restart

EXPOSE 80

ADD ./var-www-contents/u.html /var/www/u.html
ADD ./var-www-contents/u.php  /var/www/u.php

#ENTRYPOINT ["/user/sbin/apache2ctl", "-k", "restart"]

ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND"]
