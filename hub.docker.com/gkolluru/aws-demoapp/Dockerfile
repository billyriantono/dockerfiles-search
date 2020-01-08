# Simple Dockerfile
#
FROM ubuntu:16.04

RUN apt update
RUN apt install -y apache2
COPY ./index.html /var/www/html/
CMD /usr/sbin/apache2ctl -D FOREGROUND
EXPOSE 80
