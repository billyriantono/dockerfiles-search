#Version: 0.0.1
FROM ubuntu:latest

MAINTAINER Gary Zhang "lionzhang@live.cn"

RUN apt-get update
RUN apt install -y nginx
RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html

ENV LASTREFRESHED_AT = 20160827

EXPOSE 80
