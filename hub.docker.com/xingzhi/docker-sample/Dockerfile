FROM ubuntu:14.04
MAINTAINER xingzhi "xing_zhi@126.com"
ENV REFRESHED_AT 207-06-17
RUN apt-get -yqq update && apt-get -yqq install nginx
RUN mkdir -p /var/www/html/website
ADD nginx/global.conf /etc/nginx/conf.d/
ADD nginx/nginx.conf /etx/nginx/nginx.conf
EXPOSE 80