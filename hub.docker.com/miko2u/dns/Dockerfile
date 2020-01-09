FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

# packages
RUN yum -y update \
 && yum -y install bind bind-utils logrotate \
 && yum clean all \
 && cp -pr /etc/named.conf /etc/named.conf.dist
 && chkconfig named on

# expose
EXPOSE 53/udp
