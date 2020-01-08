FROM centos:7

MAINTAINER 0.1 h.kuwayama@khiten.co.jp

RUN yum -y install httpd

#ONBUILD ADD website.tar /var/www/html/

ENTRYPOINT ["/usr/sbin/httpd", "-DFOREGROUND"]
