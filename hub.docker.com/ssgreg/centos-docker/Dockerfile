FROM centos:7.4.1708
MAINTAINER me@ssgreg.com

ENV VERSION 17.05.0.ce

RUN set -ex ; \
    yum -y update ; \
    yum -y install https://yum.dockerproject.org/repo/main/centos/7/Packages/docker-engine-$VERSION-1.el7.centos.x86_64.rpm ; \
    yum -y clean all
