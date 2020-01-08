FROM centos:latest

LABEL version="0.1"

RUN yum install -y yum-utils && yum groupinstall -y development
RUN yum install -y vim wget
RUN yum update -y
RUN cd /tmp \
    && wget https://packages.chef.io/files/stable/chefdk/2.5.3/el/7/chefdk-2.5.3-1.el7.x86_64.rpm \
    && rpm -ivh chefdk-2.5.3-1.el7.x86_64.rpm \
    && rm -rf chefdk-2.5.3-1.el7.x86_64.rpm
