FROM centos:6.8
MAINTAINER retraut@gmail.com

RUN yum -y install epel-release && \
    yum -y upgrade && \
    yum -y clean all && \
    rm -fr /var/cache && \
    groupadd --gid 1111 www && \
    adduser --gid 1111 --uid 1111 --system dev
