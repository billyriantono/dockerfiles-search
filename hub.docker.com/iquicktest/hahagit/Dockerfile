FROM ubuntu:16.04
MAINTAINER jerry zhao "iquicktestsg@outlook.com"
RUN apt-get update; apt-get install -y nginx
RUN echo "Hi, I am in your container" > /var/www/html/index.html 
EXPOSE 80
WORKDIR ~/
CMD "ls"
CMD "/bin/bash"

