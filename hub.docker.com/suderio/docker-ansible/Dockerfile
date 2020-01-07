FROM centos:7
MAINTAINER Paulo Suderio paulo.suderio@gmail.com

RUN yum clean all && \
    yum -y install epel-release && \
    yum -y install PyYAML \
    python-jinja2 \
    python-httplib2 \
    python-keyczar \
    python-paramiko \
    python-setuptools \
    git \
    python-pip \
    ansible
