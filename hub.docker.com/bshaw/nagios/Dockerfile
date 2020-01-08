# Nagios
#
# VERSION 0.0.1

FROM centos:6.4
MAINTAINER Brian Shaw <bshaw@apparatus.net>

# make sure the package repository is up to date
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN yum install -y nagios

VOLUME ["/etc/nagios"]
WORKDIR /etc/nagios

ENTRYPOINT  ["/usr/sbin/nagios"]
CMD ["-v","/etc/nagios/nagios.cfg"]
