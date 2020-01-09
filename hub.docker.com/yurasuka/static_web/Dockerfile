FROM ubuntu:16.04
MAINTAINER yurasuke "yurasuka@vs77.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi you, I am in your container' \
    >/var/www/html/index.html
EXPOSE 80
