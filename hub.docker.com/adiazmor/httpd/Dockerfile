#CentOS based container
FROM centos

#Developer
MAINTAINER Aleix Diaz <aleixdzm@gmail.com>

#EXPOSE Port 80
EXPOSE 80

#RUN Commands
RUN yum -y update && yum -y install httpd && yum clean all

#Execute Apache2 in FOREGROUND
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
