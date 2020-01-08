FROM centos:centos7
MAINTAINER Andy Furnival <Andy.Furnival@gmail.com>

RUN yum update \

 	yum clean all && \

	yum install -y  epel-release \

 	yum install -y wget  \

 	yum --disablerepo="*" --enablerepo=base install tar -y \

 	yum clean all
