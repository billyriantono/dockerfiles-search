# version 1
FROM centos:7
MAINTAINER "jasonliu" "ljx407@163.com"
ENV REFRESH_AT 2019-08-25
RUN ["/bin/bash","-c","mkdir -p /var/www/html/websites/"]
RUN ["/bin/bash","-c","yum upgrade"]
RUN ["/bin/bash","-c","yum install -y epel-release && yum install -y nginx"]
ADD $PWD/nginx/global.conf /etc/nginx/conf.d/
ADD $PWD/nginx/nginx.conf /etc/nginx/nginx.conf
EXPOSE 80

