# Version: 0.0.2
FROM ubuntu:18.04
MAINTAINER tilerlgt "liguitong@aliyun.com"
RUN apt update
RUN apt install -y vim
RUN apt install -y nginx
RUN echo 'Hi, I am in your container' > /var/www/html/index.html
EXPOSE 80
