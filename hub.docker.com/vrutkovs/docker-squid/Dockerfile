FROM centos:centos7
MAINTAINER akram@free.fr
RUN yum install -y squid
ADD squid.conf /etc/squid/squid.conf
ADD run.sh /run.sh

# Make cache dirs
RUN yum install -y nc
EXPOSE 3128
VOLUME /squid
CMD /run.sh
