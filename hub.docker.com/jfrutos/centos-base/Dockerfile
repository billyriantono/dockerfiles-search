FROM centos:7
MAINTAINER jfrutos@gmail.com

RUN yum update -y \
 && yum upgrade -y \
 && yum install -y vim-minimal.x86_64 wget sudo net-tools ca-certificates unzip  \
 && yum clean all && rm -rf rm -rf /var/cache/yum
