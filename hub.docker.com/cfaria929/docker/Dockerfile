#version: 0.0.1
FROM ubuntu:16.04
MAINTAINER Christopher Faria "cfaria929@gmail.com"
RUN apt-get update; apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/var/www/html/index.html



VOLUME ["/opt/project"]
ENTRYPOINT [ "/usr/sbin/nginx" , "-g" , "daemon off;" ]
EXPOSE 80
