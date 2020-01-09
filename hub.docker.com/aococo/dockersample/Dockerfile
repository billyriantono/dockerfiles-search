FROM centos:latest

MAINTAINER 0.1 matsuda@bondstech.jp

RUN yum -y install httpd

EXPOSE 80

CMD ["/usr/sbin/httpd","-D", "FOREGROUND"]
