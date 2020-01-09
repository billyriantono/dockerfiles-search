FROM ubuntu:16.04
MAINTAINER Jay Watphisit "jwatphisit@hotmail.com"
ENV REFRESHED_AT 2014-06-01

RUN apt-get update
RUN apt-get -y -q install nginx

ADD kitten.jpg /www/data/
ADD nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]

