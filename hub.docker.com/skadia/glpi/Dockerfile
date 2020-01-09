FROM centos:7

MAINTAINER  Skadia

RUN yum update -y && yum install -y \
	httpd php php-mysql php-gd php-mbstring wget \
	&& yum clean all

RUN sed -i -e 's/^\;date\.timezone.*/date\.timezone = "Europe\/Paris"/g' /etc/php.ini
RUN sed -i -e 's/\#ServerName www.*/ServerName localhost/g' /etc/httpd/conf/httpd.conf 

ADD glpi.conf /etc/httpd/conf.d/

WORKDIR /usr/local/src/

RUN wget https://github.com/glpi-project/glpi/releases/download/0.90.3/glpi-0.90.3.tar.gz

RUN tar xzvf glpi-0.90.3.tar.gz -C /var/www/html/
RUN chown -R apache:apache /var/www/html/glpi/

CMD ["/usr/sbin/apachectl","-DFOREGROUND"]

EXPOSE 80
