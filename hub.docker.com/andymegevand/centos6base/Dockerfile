FROM centos:centos6
MAINTAINER Andy Megevand <andy.megevand@gmail.com>
RUN yum install wget tar git vim less screen ant subversion xorg-x11-server-Xvfb ant-contrib.noarch ant-nodeps telnet rng-tools lsof zip unzip traceroute tcptraceroute bc cvs ngrep sudo -y
RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -Uvh epel-release-6*.rpm
RUN curl -L https://www.getchef.com/chef/install.sh | bash
