FROM centos
MAINTAINER danling
RUN yum install httpd -y
RUN echo 'Myapp v3' > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
