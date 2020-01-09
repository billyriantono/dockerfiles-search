FROM php:7.1-apache

MAINTAINER Victors Gold Devops Team

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        libxml2-dev \
    && apt-get install -y  gnupg gnupg2 gnupg1 curl && \
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs git nano openssh-client 


ADD front /front-vg
ADD deploy.sh /

WORKDIR /etc/apache2/mods-enabled
RUN a2enmod rewrite 

ADD .htaccess  /var/www/html

WORKDIR /front-vg
RUN npm install sass-loader node-sass --save-dev && \
    npm install && \
    npm run build 


WORKDIR /
RUN chmod +x deploy.sh && \
    bash deploy.sh

WORKDIR /var/www/html

EXPOSE 80
