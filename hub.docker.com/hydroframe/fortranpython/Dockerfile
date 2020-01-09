FROM centos:7

RUN yum -y install epel-release && yum clean all && \
	yum -y install python-pip && yum clean all && \
	yum update -y && \
	yum install -y gcc-gfortran gdb make && \
	yum install -y python-devel && \
	pip install numpy && \
	yum install -y https://files.renci.org/pub/irods/releases/4.1.10/centos7/irods-icommands-4.1.10-centos7-x86_64.rpm
