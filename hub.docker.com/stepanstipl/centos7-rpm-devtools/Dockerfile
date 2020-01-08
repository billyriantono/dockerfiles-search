FROM centos:centos7
MAINTAINER Stepan Stipl
# https://github.com/stepanstipl/

RUN yum groupinstall 'Development Tools' -y
RUN yum install -y wget
RUN wget http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
RUN rpm -ivh epel-release-7-5.noarch.rpm
RUN yum install -y rpm-build gcc-c++ git rpmdevtools yum-utils
RUN mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS}

RUN mkdir /output
WORKDIR /output
