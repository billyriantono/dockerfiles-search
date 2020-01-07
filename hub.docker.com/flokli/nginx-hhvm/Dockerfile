FROM ubuntu:16.04
MAINTAINER Florian Klink <flokli@flokli.de>

RUN apt update && apt install -y nginx hhvm
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

COPY default.conf /etc/nginx/sites-available/default
COPY index.php /var/www/html/index.php
RUN chown -R www-data:www-data /var/www/html

VOLUME ["/var/www/html"]

CMD service hhvm start && nginx

WORKDIR /var/www/html

EXPOSE 80
EXPOSE 443
