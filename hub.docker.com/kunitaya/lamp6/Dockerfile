#
# LAMP old
# kunitaya/lamp:6

FROM centos:6
MAINTAINER kunitaya

RUN yum makecache fast
RUN yum -y update
RUN yum -y reinstall glibc-common

RUN localedef -v -c -i ja_JP -f UTF-8 ja_JP.UTF-8; echo "";
env LANG=ja_JP.UTF-8
RUN rm -f /etc/localtime
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN yum -y install httpd php php-* mysql-server
RUN yum clean all
