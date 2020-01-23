FROM centos:7
MAINTAINER Yefim Gasel <yefim@makonix.com>

RUN yum -y update && \
	yum -y install epel-release && \
	yum -y install tinyproxy

ADD tinyproxy.conf /etc/tinyproxy/tinyproxy.conf

ADD start.sh /start.sh

EXPOSE 8000

CMD ["/start.sh"]
