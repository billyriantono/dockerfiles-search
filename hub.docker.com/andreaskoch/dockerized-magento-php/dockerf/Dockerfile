FROM ubuntu:16.04
MAINTAINER Andreas Rammhold <andreas@rammhold.de>
MAINTAINER Florian Klink <flokli@flokli.de>

RUN apt update && apt install -y nginx hhvm
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

COPY default.conf /etc/nginx/sites-available/default
RUN mkdir -p /var/www/public
COPY index.php /var/www/public/index.php
RUN chown -R www-data:www-data /var/www/public
RUN mkdir /etc/nginx/local.conf.d

VOLUME ["/var/www/public"]

CMD service hhvm start && nginx

WORKDIR /var/www/public

EXPOSE 80
