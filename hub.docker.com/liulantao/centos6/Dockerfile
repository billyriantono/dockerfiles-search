# VERSION v1
# docker build -t="liulantao/centos7" .
FROM centos:centos6
MAINTAINER Liu Lantao <liulantao@gmail.com>
ENV REFRESHED_AT 2015-09-07
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN yum install -y http://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
RUN yum -q makecache
