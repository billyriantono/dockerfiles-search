FROM centos:centos7
RUN yum -y update
RUN yum -y install wget \
    epel-release \
    git \
    net-tools \
    openssh-server
RUN rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm
RUN yum -y install puppet
