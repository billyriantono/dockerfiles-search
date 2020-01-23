FROM ubuntu:14.04
MAINTAINER Alexander Schenkel <alex@alexi.ch>


VOLUME ["/var/www"]


RUN apt-get update && \
    apt-get install -y software-properties-common && \
    LANG=C.UTF-8 add-apt-repository ppa:ondrej/php5-5.6 && \
    apt-get update && \
    apt-get install -y \
      apache2 \
      php5 \
      php5-cli \
      libapache2-mod-php5 \
      php5-gd \
      php5-json \
      php5-ldap \
      php5-mysql \
      php5-mcrypt \
      php5-pgsql \
      php5-curl \
      php5-memcache \
      php-pear  \
      build-essential

COPY woobstores-default /etc/apache2/sites-enabled/woobstores.conf
COPY thearenamarket-default /etc/apache2/sites-enabled/thearenamarket.conf
COPY woobsresources-default /etc/apache2/sites-enabled/woobsresources.conf
COPY apache_default /etc/apache2/sites-available/000-default.conf
COPY run /usr/local/bin/run
RUN  kill -9 ps au | grep apache
RUN chmod +x /usr/local/bin/run
RUN a2enmod rewrite

EXPOSE 80
CMD ["/usr/local/bin/run"]
