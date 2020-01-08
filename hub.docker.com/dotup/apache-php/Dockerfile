FROM centos
MAINTAINER live@dotup.de
EXPOSE 80
EXPOSE 443

RUN yum update && \
    yum -y install httpd mod_ssl && \
    yum -y install php php-mysql libapache2-mod-php && \
    yum -y install wget && \
    yum -y install -y php php-mysql php-devel && \
    yum -y install epel-release && \
    yum -y install python-certbot-apache
    
RUN systemctl enable httpd.service
