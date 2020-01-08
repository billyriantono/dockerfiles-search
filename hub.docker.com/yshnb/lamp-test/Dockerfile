FROM centos:centos6

MAINTAINER yshnb

RUN yum install -y httpd
RUN yum install -y php php-devel php-cli php-mysql php-mbstring php-xml php-dom

ADD index.php /var/www/html/

RUN yum install -y mysql-server
RUN service mysqld start;

RUN yum install -y wget
RUN cd /var/www/html; wget -O index.php http://softlayer-sng.dl.sourceforge.net/project/adminer/Adminer/Adminer%204.1.0/adminer-4.1.0.php

EXPOSE 80

CMD mysqld_safe & apachectl -DFOREGROUND
