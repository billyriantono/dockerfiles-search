FROM debian:jessie
MAINTAINER Marcel Boogert <marcel@mtdb.nl>

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install \
        apache2 php5 php5-mysql php5-mcrypt php5-memcache php5-curl php5-memcached php5-apcu php5-gd zip mcrypt ssmtp
RUN apt-get clean

RUN \
    a2enmod headers && \
    a2enmod rewrite && \
    a2enmod expires

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data

EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND
