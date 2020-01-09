FROM ubuntu:18.04
LABEL maintainer="remfath@gmail.com"
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
RUN apt update; apt install -y nginx
RUN echo 'Hi, I am in your container. Hello World!' > /var/www/html/index.html
EXPOSE 80
