# CentOS
#
# VERSION               0.0.1

FROM     centos:latest

MAINTAINER Bithedz "bithedz@gmail.com"
#change repo to local, delete it before build if you don't have local repo

RUN yum install -y \
    epel-release \
    iproute \
    openssl-devel \
    readline-devel\
    zlib-devel \
    wget \
    curl \
    git \
    dtach \
    nano \
    hash-slinger \
    bzip2 \
    tar \
    perl \
    libffi-devel \
    libxslt-devel \
    redis \
    python \
   
&&  yum groupinstall "Development Tools" -y \
&&  yum clean all
