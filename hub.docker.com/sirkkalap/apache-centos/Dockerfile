FROM centos:6.6

MAINTAINER Petri Sirkkala "sirpete@iki.fi"

RUN yum -y update && yum -y install httpd && yum -y clean all # 2015-03-28

ENV APACHE_RUN_USER apache
ENV APACHE_RUN_GROUP apache
ENV APACHE_LOG_DIR /etc/httpd/logs/

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

