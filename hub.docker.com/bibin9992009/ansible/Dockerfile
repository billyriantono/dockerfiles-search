FROM centos:centos7
MAINTAINER bibin9992009 <bibin9992009@gmail.com>
RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install vim PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools git python-pip
RUN yum -y install ansible
EXPOSE 22 
WORKDIR /etc/ansible

