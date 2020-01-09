FROM centos:latest

MAINTAINER 0.1 zhuzheben@hotmail.com

RUN yum -y install httpd

ADD html/ /var/www/html/

CMD /user/sbin/httpd -d foreground
