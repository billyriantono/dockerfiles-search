# Version: 0.0.1
From centos
MAINTAINER Shen Ping "jsksnick@163.com"
#RUN yum update
RUN rpm -ivh https://mirrors.tuna.tsinghua.edu.cn/epel/7/x86_64/e/epel-release-7-9.noarch.rpm
#RUN rpm -ivh https://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN yum install -y nginx
RUN echo 'Hi,I am in your container' >/usr/share/nginx/html/index.html
EXPOSE 80
