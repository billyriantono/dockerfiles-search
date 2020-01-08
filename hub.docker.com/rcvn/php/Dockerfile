FROM rcvn/centos:7.1

MAINTAINER RCVN nguyen.tuankhanh@rivercrane.vn

## Add Repos: remi, epel
RUN rpm -Uvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

## Install php 5.6
RUN yum --enablerepo=remi,remi-php56 -y install php php-common
RUN yum --enablerepo=remi,remi-php56 -y install php-mysql php-pear php-gd php-mcrypt php-ldap php-xcache php-devel php-mbstring php-pdo php-pecl-xdebug php-pecl-memcache php-xml php-process libcurl-devel libxml2-devel mod_ssl pcre-devel

## Uninstall httpd server attached in remi package
RUN yum -y erase httpd

CMD ["/bin/bash"]