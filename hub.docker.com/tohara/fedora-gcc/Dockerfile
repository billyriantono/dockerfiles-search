FROM fedora:latest

MAINTAINER Tomochika Hara <dockerhub@thara.jp>

RUN yum -y update && yum clean all

RUN yum groupinstall -y "Development Tools" ; yum clean all
RUN yum install -y gcc-c++
