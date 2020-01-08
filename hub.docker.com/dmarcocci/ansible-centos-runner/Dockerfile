FROM centos:7

RUN yum update -y && \
    yum install -y epel-release

RUN yum install -y python2-pip && \
    pip install --upgrade pip && \
    pip install ansible==2.7.5
