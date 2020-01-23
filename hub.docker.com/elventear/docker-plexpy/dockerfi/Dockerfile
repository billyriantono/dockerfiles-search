FROM centos
MAINTAINER Elsa
RUN yum install httpd -y
RUN echo 'myapp v1' > /var/www/html/index.html
EXPOSE 80
CMD ["/user/sbin/httpd","-D","FOREGROUND"]
