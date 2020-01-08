# Latest version of centos 6
FROM centos:centos6
MAINTAINER Shawn Hsiao <shawn.hsiao@gmail.com>
RUN yum clean all && \
    yum -y install wget && \
    wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm && \
    rpm -Uvh epel-release-latest-6.noarch.rpm && \
    rm -f epel-release-latest-6.noarch.rpm && \
    yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools git python-pip ansible && \
    yum -y install sudo
