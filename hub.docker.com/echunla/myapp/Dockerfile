FROM centos
MAINTAINER John
RUN yum install -y httpd
RUN echo 'myapp v1' > /var/www/html/index.html
EXPOSE 80
CMD ["/user/sbin/httpd", "-D", "FOREGROUND"]
