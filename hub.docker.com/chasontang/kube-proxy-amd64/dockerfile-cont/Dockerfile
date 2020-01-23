FROM centos:centos7

MAINTAINER Charles Chen <charlestg@yahoo.com>

RUN yum -y update && \
    yum install -y epel-release && \
    yum clean all

RUN rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro 
RUN rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
RUN yum install ffmpeg ffmpeg-devel -y