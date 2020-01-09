#Version 1.0
FROM centos:latest

MAINTAINER allonkwok <allonkwok@qq.com>

#设置root用户为后续命令的执行者
USER root

#执行操作
RUN yum update -y
RUN yum install initscripts -y
RUN yum install epel-release -y
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
RUN yum install php72w-fpm php72w-opcache php72w-gd php72w-common php72w-mbstring php72w-mysqlnd php72w-pear php72w-pecl-igbinary php72w-pecl-memcached php72w-pecl-mongodb php72w-pecl-redis php72w-pgsql php72w-xml php72w-xmlrpc -y