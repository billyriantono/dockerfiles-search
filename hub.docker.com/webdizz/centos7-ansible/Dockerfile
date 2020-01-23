FROM centos:7

MAINTAINER Izzet Mustafaiev "izzet@mustafaiev.com"

# Set correct environment variables.
ENV	HOME /root
ENV	LANG en_US.UTF-8
ENV	LC_ALL en_US.UTF-8

RUN yum clean all \
    && yum -y install epel-release \
    && yum -y install PyYAML python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools git python-pipe \
    && yum -y install python-simplejson tar unzip git \
    && yum -y install ansible \
    && yum clean all

RUN mkdir -p /opt/ansible/library
ENV PATH /bin:/usr/bin:/sbin:/usr/sbin
ENV ANSIBLE_LIBRARY /opt/ansible/library