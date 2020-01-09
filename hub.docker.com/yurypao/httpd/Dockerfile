FROM centos

MAINTAINER pao.d.preciosit@gmail.com

EXPOSE 80

RUN yum -y update && yum -y install httpd && yum clean all

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
