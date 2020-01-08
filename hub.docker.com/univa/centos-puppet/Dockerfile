FROM centos:7

MAINTAINER engineering@univa.com

RUN rpm -ivh http://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
RUN yum -y install puppet-agent hostname
RUN yum -y install epel-release
RUN yum -y install python36
RUN yum -y install git

CMD ["/usr/bin/true"]
