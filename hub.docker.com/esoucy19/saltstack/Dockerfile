FROM centos:7
MAINTAINER Etienne Soucy

RUN yum clean all && \
  yum install -y yum install epel-release && \
  yum install -y https://repo.saltstack.com/yum/redhat/salt-repo-latest-2.el7.noarch.rpm && \
  yum update -y && \
  yum install -y sudo git salt-master salt-minion && \
  yum clean all
