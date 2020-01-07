FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && apt-get -y upgrade

RUN apt-get -y install apache2 libapache2-mod-security2 libapache2-mod-evasive
RUN apt-get -y install php7.0 libapache2-mod-php7.0 php7.0-mcrypt php7.0-mysql php-redis php7.0-curl php7.0-xmlrpc php7.0-xml
RUN apt-get -y install php-xdebug
RUN apt-get -y install wget

RUN apt-get clean

ENV ADMIN_EMAIL dt@mbc-design.dk
ENV SERVER_NAME example.com

COPY 01-security.ini /etc/php/7.0/apache2/conf.d/
COPY security.conf /etc/apache2/conf-available/
COPY 000-default.conf /etc/apache2/sites-available/

RUN a2enmod rewrite
RUN a2enmod headers

#COPY setup.py /tmp/
#CMD python3 /tmp/setup.py
#CMD rm -f /tmp/setup.py

EXPOSE 80

VOLUME /var/www
VOLUME /tmp/profile

CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]
