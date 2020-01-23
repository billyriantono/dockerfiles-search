FROM h2sp/cent65_base
MAINTAINER Shuichi Takaoka <htwosp@gmail.com>

RUN echo "NETWORKING=yes" > /etc/sysconfig/network
RUN rpm -ihv http://ftp.riken.jp/Linux/fedora/epel/6/i386/epel-release-6-8.noarch.rpm
RUN yum -y update
RUM yum -y install R
RUN wget http://download2.rstudio.org/rstudio-server-0.98.501-x86_64.rpm
RUN yum -y install --nogpgcheck rstudio-server-0.98.501-x86_64.rpm
