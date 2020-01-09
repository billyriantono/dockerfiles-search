FROM centos:7.2.1511

RUN yum install -y git-all \
    && yum -y groupinstall "Development Tools" \
    && yum -y install gcc \
    && yum clean all