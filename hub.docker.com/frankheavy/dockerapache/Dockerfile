FROM eboraas/apache
MAINTAINER Frank Munoz <frank@munoz.com>
RUN apt-get update
RUN apt-get -y install vim
RUN apt-get -y install gcc
RUN apt-get -y install nano
RUN echo Mi primer Docker
COPY 000-default.conf /etc/apache2/sites-available/
COPY index.html /var/www/html/
