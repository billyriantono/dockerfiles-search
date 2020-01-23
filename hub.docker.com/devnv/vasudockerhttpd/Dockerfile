FROM centos:7
MAINTAINER vasudevn "npadma09@gmail.com"
RUN yum install httpd -y
RUN apachectl
RUN echo 'Our first Docker image for Centos7 webpage' > /var/www/html/index.html
EXPOSE 80
CMD ["/usr/sbin/httpd", "-g", "daemon off;"]
