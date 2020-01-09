FROM ubuntu:16.04
MAINTAINER Alex Tymchenko <alex@beedevs.com>

RUN apt-get update
RUN apt-get install -y nano \
curl \
supervisor \
unzip \
composer \
nano

RUN mkdir -p /root/logs
ADD supervisord.conf /root/supervisord.conf

RUN apt-get install -y apache2
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
ADD 000-default.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

RUN echo "mysql-server mysql-server/root_password password 12345" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password 12345" | debconf-set-selections
RUN apt-get install -y mysql-server

RUN apt-get install -y php7.0 \
libapache2-mod-php7.0 \
php7.0-mysql \
php7.0-mbstring \
php7.0-curl \
php7.0-cli \
php7.0-xml

VOLUME [“/var/www/html”, “/root/logs”]
EXPOSE 80 3306
CMD /usr/bin/supervisord -c /root/supervisord.conf
RUN apt-get clean