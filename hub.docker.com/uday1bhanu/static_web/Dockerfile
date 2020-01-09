#version .0.1
FROM ubuntu:16.04
MAINTAINER Uday Bhanu Prasad "uday1bhanu@gmail.com"
RUN apt-get update; apt-get install -y nginx;
RUN echo 'Hi! Welcome to MilkyWay Galaxy!' > /var/www/html/index.html
EXPOSE 80
CMD [ "/bin/bash" ]
