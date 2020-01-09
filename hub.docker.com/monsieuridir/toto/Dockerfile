FROM centos
MAINTAINER Idir Tir <idir.tir@gmail.com>
LABEL version="1.0"
LABEL description="Base image for the Openstack installation"
LABEL readme="this image is used as the base for installing all Openstack components"

RUN yum update -y
RUN yum install -y net-tools.x86_64 iputils.x86_64 curl.x86_64 && \
        yum clean all
