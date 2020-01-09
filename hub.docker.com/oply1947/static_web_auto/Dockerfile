# Version 0.0.4
FROM ubuntu:latest
ENV VERSION 0.0.4
MAINTAINER Oply 1947 'oply1947@teleworm.us'
RUN apt-get update
RUN apt-get install -y nginx
WORKDIR /var/www/html
RUN echo 'Hi, I am in your container' ${VERSION} > index.html
CMD nginx -g 'daemon off;'
EXPOSE 80
