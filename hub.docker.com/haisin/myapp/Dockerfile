FROM centos
MAINTAINER Haisin
RUN yum install -y httpd
RUN echo 'myapp v1' > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
