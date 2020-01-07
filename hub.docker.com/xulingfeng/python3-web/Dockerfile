FROM centos:latest
MAINTAINER xulingfeng "xulingfengcn@gmail.com"
RUN yum install -y gcc automake autoconf libtool make gcc-c++
RUN yum install -y wget
RUN yum install -y openssl-devel
RUN wget https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tgz -P /software/
RUN tar -zxvf /software/Python-3.5.2.tgz -C /software/
RUN cd /software/Python-3.5.2 && ./configure && make -j2&& make install -j2
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools
RUN pip3 install Django Flask requests PyMySQL ldap3 jira celery simplejson
