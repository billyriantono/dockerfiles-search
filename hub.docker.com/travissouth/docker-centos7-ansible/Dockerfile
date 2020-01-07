FROM geerlingguy/docker-centos7-ansible
MAINTAINER Irvin Capagcuan <irvin@capagcuan.org>

RUN yum -y update; yum clean all; \
	yum makecache fast; \
	yum install git openssh-server -y; \
	yum clean all
