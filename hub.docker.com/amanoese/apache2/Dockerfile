FROM ubuntu

MAINTAINER amanoese<amanoese@gmail.com>

RUN apt-get update && apt-get install -y apache2
RUN echo ServerName localhost > /etc/apache2/conf-available/fqdn.conf
RUN a2enconf fqdn
RUN cp /var/www/html/index.html /var/www/html/hoge.html

EXPOSE 80
CMD apachectl -DFOREGROUND
