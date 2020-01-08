FROM centos:7

MAINTAINER sky91 - feitiandaxia1991@163.com

COPY galera.repo /etc/yum.repos.d/galera.repo

RUN	yum -y update \
	&& yum -y install which galera-3 mysql-wsrep-5.6

COPY my.cnf /etc/mysql/my.cnf
