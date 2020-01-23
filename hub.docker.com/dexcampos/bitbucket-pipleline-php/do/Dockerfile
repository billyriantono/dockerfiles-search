FROM centos:7
MAINTAINER devteam-general@rcp.pe
ENV PYTHONUNBUFFERED 1

# Install Python and tools
RUN yum -y update && yum clean all \
	&& yum -y install epel-release && yum clean all \
	&& yum -y install postgresql-devel && yum clean all \
	&& yum -y install python-devel python-setuptools python-pip python-lxml && yum clean all \
	&& yum -y install mysql-devel && yum clean all \
	&& pip install --upgrade pip \
	&& yum -y install gcc gcc-c++ \
	&& yum clean all \
	&& yum -y reinstall glibc-common  \
	&& yum clean all 

ENV TZ America/Lima
