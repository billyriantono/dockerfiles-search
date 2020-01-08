FROM centos:centos6

ENV PUPPET_VERSION 3.7.3
ENV HIERA_VERSION 1.3.4

VOLUME /puppet

RUN yum localinstall -y http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm && \
    yum install -y puppet-${PUPPET_VERSION} hiera-${HIERA_VERSION} && \
	yum clean all && \
	find /etc/yum.repos.d/ -iname '*puppet*' -exec rm -f {} \;

