# from images
FROM centos:latest

# maintainer name
MAINTAINER 0.1 your-name@your-domain.com

# apache httpd install
RUN ["yum", "install", "-y", "httpd"]

# apache httpd exec
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
