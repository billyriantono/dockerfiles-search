FROM php:5.6-apache-jessie

LABEL maintainer "Minh Nguyen <ndminh9x@gmail.com>"

# Update & install dev tools necessary
RUN apt-get update
RUN apt-get install libssl-dev -y

# Install the mongo driver
RUN pecl install mongo
ADD mongo.ini /usr/local/etc/php/conf.d/mongo.ini

EXPOSE 80/tcp

CMD apache2ctl -D FOREGROUND
