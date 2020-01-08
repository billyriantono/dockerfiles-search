FROM centos:7
LABEL MAINTAINER "jaron@rubensteintech.com"

# update to latest packages and install CentOS Development tools
RUN yum -y update && \
    yum -y groupinstall 'Development tools' && \
    yum -y install which openssh-clients && \
    yum clean all
