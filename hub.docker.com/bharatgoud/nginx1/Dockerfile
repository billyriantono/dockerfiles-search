# Installing Nginx
FROM centos
RUN yum update -y
ADD /nginx.repo  /etc/yum.repos.d/nginx.repo
RUN yum install epel-release -y
RUN yum install nginx -y
RUN yum install wget -y
RUN yum install telnet -y
EXPOSE 80

