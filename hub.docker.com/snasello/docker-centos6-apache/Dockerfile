# CentOS 6.4 + Apache
#
# VERSION 0.0.1
#

FROM centos:6.4

MAINTAINER Samuel Nasello <samuel.nasello@elosi.com>

# install apache
RUN yum install -y httpd

# volumes
VOLUME ["/var/www"]

# Ports
EXPOSE 80

# EXEC
CMD ["-D", "FOREGROUND"]
ENTRYPOINT ["/usr/sbin/httpd"]
