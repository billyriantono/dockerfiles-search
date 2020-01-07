# base image
FROM centos:centos7

# writer infomation
MAINTAINER veggente

RUN yum -y install httpd

ONBUILD ADD index.html /var/www/html

CMD /sbin/httpd -D FOREGROUND
