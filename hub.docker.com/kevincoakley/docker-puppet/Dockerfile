FROM centos:latest
MAINTAINER Kevin Coakley <kcoakley@sdsc.edu>

RUN rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
RUN yum install puppet-agent-1.10.10 bundle rubygem-bundler ruby-devel rubygem-rake -y