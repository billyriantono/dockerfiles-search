FROM centos:latest
MAINTAINER Jasper Aikema <jaikema@it-ernity.nl>

# Update base image
RUN yum -y update && yum clean all

# Install EPEL
RUN yum -y install epel-release

# Install the ius repo
RUN rpm -ivh https://centos7.iuscommunity.org/ius-release.rpm
RUN rpm --import /etc/pki/rpm-gpg/IUS-COMMUNITY-GPG-KEY

# Update latest packages
RUN yum -y update && yum clean all && rm -rf /var/cache/yum
