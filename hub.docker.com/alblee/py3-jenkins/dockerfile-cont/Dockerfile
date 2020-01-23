FROM centos
MAINTAINER Alben
RUN yum install httpd -y
RUN echo 'Myapp v1 --> xxx' > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
