FROM apriorit/docker-centos7-x64
MAINTAINER Apriorit

USER root
RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm
RUN yum update -y
RUN yum install -y deltarpm python35u-3.5.2 python35u-pip  python35u-devel gcc mysql-devel libxml2-devel libxslt-devel \
 libmcrypt-devel libcurl-devel \ && yum clean all

ENV PYCURL_SSL_LIBRARY=nss
RUN pip3.5 install pycurl  --no-cache-dir
