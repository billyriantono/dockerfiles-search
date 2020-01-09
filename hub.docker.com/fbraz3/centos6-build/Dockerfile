FROM centos:6

RUN yum install -y rpm-build vim wget

RUN wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo
RUN yum install -y devtoolset-2-gcc devtoolset-2-binutils devtoolset-2-gcc-c++

RUN yum groupinstall -y 'Development Tools'
RUN yum install -y readline-devel zlib-devel
RUN yum install -y epel-release
RUN yum install -y yum-utils
