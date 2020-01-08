FROM itdevdixons/ubuntu:14.04

MAINTAINER Viliam Husar viliam.husar@dixonscarphonegroup.com

ENV DEBIAN_FRONTEND noninteractive

# Install apache
RUN apt-get update && apt-get -y install apache2

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN rm /etc/apache2/sites-available/*
RUN rm /etc/apache2/sites-enabled/*
RUN a2enmod rewrite
RUN a2enmod proxy
RUN a2enmod proxy_fcgi
RUN a2enmod headers

ADD apache2/sites-available /etc/apache2/sites-available/


ADD run.sh /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

VOLUME /var/www

ADD run.sh /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

EXPOSE 80

CMD /usr/local/bin/run