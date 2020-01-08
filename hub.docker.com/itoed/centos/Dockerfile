FROM centos:6.6
MAINTAINER Eduardo Ito <itoed@yahoo.com>

# Update packages
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
RUN yum update -y; yum clean all

# EPEL Repository
RUN yum install -y epel-release; yum clean all
RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
