FROM ubuntu:16.04
MAINTAINER Karthik "karthik.network@gmil.com"
ENV REFRESHED_AT 2016-06-08
RUN apt-get update
RUN apt-get -y -q install nginx
RUN apt-get -y install  php7.0-fpm
RUN mkdir -p /var/www/html
ADD nginx/global.conf /etc/nginx/conf.d/
ADD nginx/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
