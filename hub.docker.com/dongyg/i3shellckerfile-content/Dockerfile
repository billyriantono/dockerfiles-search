FROM centos:latest

MAINTAINER DonaldSimpson<at>GMail<dot>com

# base CentOS Docker image with Java and base dev tools

RUN yum update -y &&\
	yum install -y java-1.8.0-openjdk \
				git \
        bzip2 \
        unzip \
        wget &&\
    yum clean all
