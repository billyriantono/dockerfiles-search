FROM tutum/apache-php

MAINTAINER Luis Herrera <luis.herrera.ec@gmail.com>

RUN apt-get update
RUN apt-get install -y  nano
RUN a2enmod rewrite
COPY apache2.conf /etc/apache2/

EXPOSE 80 443

