FROM centos:7
MAINTAINER Nozomu Kaneko <nozom.kaneko@gmail.com>

RUN yum update -y && \
    yum install -y httpd mod_wsgi && \
    yum clean all

EXPOSE 80
CMD ["/usr/sbin/apachectl", "-DFOREGROUND"]
