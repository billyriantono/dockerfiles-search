FROM ubuntu:13.10

MAINTAINER Geoffroy Lorieux <geoffroy@techmantra.co>

RUN echo "deb http://archive.ubuntu.com/ubuntu/ raring main universe" >> /etc/apt/sources.list

RUN apt-get update

RUN apt-get install -y nano wget dialog net-tools

RUN apt-get install -y nginx

RUN rm -v /etc/nginx/nginx.conf

ADD nginx.conf /etc/nginx/

EXPOSE 80

CMD service nginx start
