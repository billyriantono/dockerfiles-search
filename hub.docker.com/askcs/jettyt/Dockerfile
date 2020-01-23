FROM centos:centos6
MAINTAINER ashok <ashok.thota62@gmail.com>

RUN yum -y update; yum clean all
RUN yum -y install httpd

RUN echo "my sample server" >> /var/www/html/index.html
RUN yum -y install php
EXPOSE 80


RUN echo "/sbin/service httpd start" >> root/.bashrc

