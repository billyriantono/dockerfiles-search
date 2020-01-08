FROM centos:7.5.1804
MAINTAINER buddyingdevelopment <development@buddying.jp>

# Packages
RUN yum -y update && yum clean all
RUN yum -y install epel-release
RUN yum reinstall -y glibc-common
RUN yum clean all

# Networking
RUN echo 'NETWORKING=yes' > /etc/sysconfig/network

# Local
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime
RUN echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock