FROM centos:latest
USER root
MAINTAINER Nikhil Anil Kumar <nikhil.aniill@gmail.com>
RUN yum -y update 
RUN yum -y install httpd
RUN echo "The Web Server is running." > /var/www/html/index.html
EXPOSE 80
CMD ["-D","FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]

