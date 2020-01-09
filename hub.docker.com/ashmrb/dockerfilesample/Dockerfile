#STEP:0 CentOS(base image)
FROM centos:latest

#Option:Mainteiner info
MAINTAINER Mrb Ash loadforonly@hotmail.co.jp

#STEP:1 install Apache
RUN yum install -y httpd

#STEP:2 copy files
#COPY index.html /var/www/html/

#STEP:3 start Apache
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
