FROM centos
MAINTAINER Jacky
RUN yum install httpd -y; yum clean all
RUN echo 'Hi man v1.0.' >/var/www/html/index.html
EXPOSE 80 443
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
