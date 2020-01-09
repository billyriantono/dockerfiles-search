FROM centos
MAINTAINER sguphil
RUN yum install httpd -y
RUN echo 'Myapp v2' > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
