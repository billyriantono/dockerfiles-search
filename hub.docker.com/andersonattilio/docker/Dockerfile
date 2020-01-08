FROM centos:7

MAINTAINER Anderson Attilio <aattilio.sousa@gmail.com>

RUN yum update -y && \ 
	yum -y install httpd && \
        yum -y install php && \
	yum -y install php-mysql && \
	yum -y install wget && \
        yum -y install unzip && \
	cd /var/www/html && \
	wget "https://br.wordpress.org/wordpress-4.6.1-pt_BR.zip" && \
	unzip wordpress-4.6.1-pt_BR.zip && \
        rm -f wordpress-4.6.1-pt_BR.zip

COPY info.php /var/www/html/info.php

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
