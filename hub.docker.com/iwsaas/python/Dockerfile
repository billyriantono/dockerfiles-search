FROM iwsaas/centos:7.1
MAINTAINER Henry Huang <henry.s.huang@gmail.com>

RUN yum -y update; yum clean all
RUN yum -y ca-certificates; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install python-pip; yum clean all

ADD . /src

RUN cd /src; pip install -r requirements.txt
