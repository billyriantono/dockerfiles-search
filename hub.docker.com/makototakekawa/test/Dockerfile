FROM centos
MAINTAINER Admin <admin@admin.com>

CMD echo "now running..."

RUN yum install -y httpd
ADD ./index.html /var/www/html/

EXPOSE 80
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]