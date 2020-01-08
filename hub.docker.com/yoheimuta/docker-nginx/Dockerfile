FROM ubuntu:14.04
MAINTAINER Yohei Yoshimuta "yoheimuta@gmail.com"
ENV REFRESHED_AT 2014-09-16
RUN apt-get update
RUN apt-get -y -q install nginx
RUN mkdir -p /var/www/html
ADD global.conf /etc/nginx/conf.d/
ADD nginx.conf /etc/nginx/nginx.conf
EXPOSE 80
