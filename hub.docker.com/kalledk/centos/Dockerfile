FROM centos:7

MAINTAINER Kalle R. Møller

COPY files/yum_saved.txt /tmp/yum_saved.txt

RUN yum -y load-transaction /tmp/yum_saved.txt \
    && yum -y clean all
