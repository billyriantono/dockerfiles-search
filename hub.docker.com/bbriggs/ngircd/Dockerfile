# ngIRCd
# Version 0.1
#This guy did it better:
#https://github.com/rbjarnason/docker-ngircd

FROM centos:6.6
MAINTAINER Bren Briggs <briggs.brenton@gmail.com>

RUN yum install -y python-setuptools epel-release
RUN yum install -y ngircd
RUN easy_install supervisor
RUN mkdir -p /var/log/supervisord
ADD supervisord.conf /etc/supervisord.conf

ENTRYPOINT ["/usr/bin/supervisord", "-n"]