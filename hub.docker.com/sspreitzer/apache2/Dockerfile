FROM ubuntu:14.04.1

MAINTAINER Sascha Spreitzer <sascha@spreitzer.ch>

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y apache2
RUN a2enmod ssl
RUN a2ensite default-ssl

ADD apache2-start /usr/local/sbin/

CMD ["apache2-start"]

EXPOSE 80
EXPOSE 443

VOLUME /var/www
VOLUME /var/www/html
VOLUME /etc/apache2

