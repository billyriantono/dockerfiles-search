FROM php-zendserver:8.5
MAINTAINER Monty Chase <monty.chase@me.com>

RUN apt-get -y update && \
    apt-get -y install \
    vim

# Replace default with custom Dev VirtualHost
RUN rm /etc/apache2/sites-available/000-default.conf
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf
