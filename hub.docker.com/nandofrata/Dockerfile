FROM centos

RUN yum -y update
RUN yum install -y nano vim net-tools httpd 
RUN yum install -y php php-mysql libzip php-cli php-common php-pdo

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

# PHPINFO
ADD phpinfo.php /var/www/html/phpinfo.php

EXPOSE 80 

CMD ["/run-httpd.sh"]
