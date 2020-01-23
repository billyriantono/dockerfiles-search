FROM php:7.1.8-apache
MAINTAINER Adil 

COPY ./ /srv/app

#install git
RUN apt-get update \
    && apt-get install -y git
    
RUN chown -R root:root /srv/app \
    && a2enmod rewrite