  FROM centos
  MAINTAINER mikezh15
  RUN yum install httpd -y
  RUN echo 'Myapp v1' > /var/www/html/index.html
  EXPOSE 80
  CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
  RUN echo "End of dockerfile=="
