FROM phusion/baseimage:latest
MAINTAINER Vrakfall <jeremy@artphotolaurent.be>

RUN mkdir /var/www && \
    mkdir /var/www/html

RUN apt-get update && \
    apt-get -y install \
    apache2 \
    libapache2-mod-php5 \
    sendmail \
    openssh-server \
    php5-mysql \
    php5-gd \
    php5-curl \
    php-pear \
    php-apc \
    php5-mcrypt

COPY php.ini /etc/php5/apache2/php.ini
COPY apache_default /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

VOLUME ["/var/www/html/"]

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
