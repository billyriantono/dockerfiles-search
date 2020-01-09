FROM centos:latest
USER root
MAINTAINER Nilita Anil Kumar <nilita.aniill@gmail.com>
RUN yum -y update 
RUN yum -y install httpd
RUN echo "the web server is running. " > /var/www/html/index.html
EXPOSE 80
CMD ["-D","FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]
