FROM ubuntu:latest
MAINTAINER Edson Lima <edson@homebrasil.com>

RUN apt-get update
RUN apt-get install -y apache2 php5 php5-cli php5-readline php5-mysql

RUN a2enmod rewrite
RUN a2enmod php5
ADD apache2.conf /etc/apache2/apache2.conf
ADD bootstrap.sh /bootstrap.sh
RUN chmod 755 /bootstrap.sh

EXPOSE 80
CMD ["/bootstrap.sh"]