FROM centos:latest

ENV PDK_VERSION=1.0.1.0

RUN yum -y install https://puppet-pdk.s3.amazonaws.com/pdk/${PDK_VERSION}/repos/el/7/PC1/x86_64/pdk-${PDK_VERSION}-1.el7.x86_64.rpm
RUN yum -y install git
RUN yum clean all
