# Set the base image to centos6.8
FROM centos:6.8

# File Author / Maintainer
MAINTAINER lvyalin lvyalin.yl@gmail.com

RUN yum -y install dnsmasq && yum clean all

COPY dnsmasq.conf /etc/
ENTRYPOINT ["dnsmasq", "-d"]