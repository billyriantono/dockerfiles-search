FROM centos:latest

WORKDIR /root/data/
COPY ./centos/CentOS-Base.repo /root/data
RUN mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.bak \
	&& cp /root/data/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo \
	&& yum clean all && yum makecache && yum -y update \
	&& yum -y install tar vim iproute  \
	&& echo "alias ll='ls -l'"  >> ~/.bashrc \
	&& rm -rf /root/data/CentOS-Base.repo \
	