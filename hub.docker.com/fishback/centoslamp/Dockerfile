FROM centos:6
MAINTAINER Thatcher Peskens <zhouliang606@gmail.com>

RUN rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm
# install httpd
RUN yum -y install httpd

# install mysql
RUN yum install -y mysql mysql-server
RUN echo "NETWORKING=yes" > /etc/sysconfig/network

# install php
RUN yum -y install php56w php56w-bcmath php56w-cli php56w-common php56w-devel php56w-embedded php56w-enchant php56w-fpm php56w-gd php56w-imap php56w-intl php56w-mbstring php56w-mcrypt php56w-mysql php56w-opcache php56w-pdo php56w-pear php56w-soap php56w-tidy php56w-xml php56w-xmlrpc

# start mysqld to create initial tables
ENTRYPOINT service mysqld start && service httpd start && /bin/bash
ADD phpinfo.php /var/www/html/
EXPOSE 22 80 3306