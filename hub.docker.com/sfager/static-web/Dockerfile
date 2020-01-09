# Version 0.0.1
FROM ubuntu:14.04
MAINTAINER Stephen Fager "sfagerca82@yahoo.com"
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get install -y subversion
RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html
EXPOSE 80
