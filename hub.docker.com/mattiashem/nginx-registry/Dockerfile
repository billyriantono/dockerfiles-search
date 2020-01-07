#Base docker file for lifeandshell.com
FROM centos:7
MAINTAINER "Mattias Hemmingsson" <matte.hemmingsson@gmail.com>

EXPOSE 80
EXPOSE 443

#Install deps
RUN yum install epel-release -y
RUN  yum -y install nginx
RUN yum install httpd-tools -y
ADD nginx.conf /etc/nginx/nginx.conf
ADD configs/ssl /etc/nginx/ssl
ADD start.sh /opt/start.sh
RUN chmod +x /opt/start.sh 
CMD /opt/start.sh
