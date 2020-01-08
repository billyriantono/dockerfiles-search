FROM centos:5

RUN yum install -y curl wget make file which
RUN rpm -ivh http://dl.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm
COPY devtools64.repo /etc/yum.repos.d/devtools64.repo
COPY devtools32.repo /etc/yum.repos.d/devtools32.repo
RUN yum install -y devtoolset-2-{gcc,gcc-c++,binutils} git python26
RUN yum install -y glibc-devel.i386 devtoolset-2-libstdc++-devel.i386

ENV PATH /opt/rh/devtoolset-2/root/usr/bin:$PATH
