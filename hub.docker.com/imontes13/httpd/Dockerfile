FROM centos:7

MAINTAINER Iván Montes Nicolás <imontes@ilg.cat>

# Install Apache

RUN yum update -y
RUN yum install -y httpd httpd-tools
RUN yum clean all

EXPOSE 80

# Start Apache
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]


