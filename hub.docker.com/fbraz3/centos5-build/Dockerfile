FROM fatherlinux/centos5-base

COPY repo-files/*.repo /etc/yum.repos.d/

RUN yum install -y rpm-build
RUN yum groupinstall -y 'Development Tools'
RUN yum install -y readline-devel zlib-devel

