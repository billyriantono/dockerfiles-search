FROM centos:centos7

RUN yum -y install httpd php php-devel php-pear php-pdo php-mysqlnd php-mbstring php-gd
    
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]