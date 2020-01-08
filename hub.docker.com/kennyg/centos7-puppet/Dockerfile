FROM centos:centos7
MAINTAINER Kenny Gatdula "kennygatdula@gmail.com"

RUN yum -y update && yum clean all

RUN rpm -ivh https://yum.puppetlabs.com/el/7/products/x86_64/puppetlabs-release-7-11.noarch.rpm

RUN yum -y install puppet

RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc
RUN gem install librarian-puppet

