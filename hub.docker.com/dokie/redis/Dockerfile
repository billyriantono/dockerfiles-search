# redis Server
#
# VERSION 0.0.1

# Building from CentOS 7
FROM centos:centos7
MAINTAINER i2O Water <anapos@i2owater.com>

RUN yum -y update; yum clean all
RUN yum -y install wget
RUN wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-2.noarch.rpm
RUN rpm -ivh epel-release-7-2.noarch.rpm
RUN yum -y install redis

EXPOSE      6379
CMD  ["/usr/bin/redis-server"]

