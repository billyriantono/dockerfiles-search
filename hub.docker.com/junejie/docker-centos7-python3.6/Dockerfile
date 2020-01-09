FROM centos:7

LABEL maintainer="junejieruzol1@gmail.com"

RUN yum update -y
RUN yum -y install yum-utils
RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm
RUN yum -y install python36u
RUN python3.6 -V
RUN yum -y install python36u-pip
RUN pip3.6 install virtualenv