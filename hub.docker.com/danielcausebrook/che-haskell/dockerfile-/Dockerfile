#
# MAINTAINER        Steve <daneiyunzhijia@163.com>
# DOCKER-VERSION    1.12.1
#
# Dockerizing CentOS7: Dockerfile for building CentOS images
#
FROM       centos:7
MAINTAINER Steve <daneiyunzhijia@163.com>

ENV TZ "Asia/Shanghai"
ENV TERM xterm

RUN yum clean all && yum repolist
RUN yum install -y curl wget vim-enhanced yum-utils  net-tools gcc gcc-c++ git make automake 


CMD ["/bin/bash"]
