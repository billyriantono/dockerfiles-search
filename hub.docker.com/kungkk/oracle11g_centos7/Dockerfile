FROM    centos:7
MAINTAINER "kkk" <kkk@jccsoftware.com>
RUN	mkdir -p /run/lock/subsys; \
	yum check-update; \
	yum update; \
	yum install -y libaio bc flex net-tools; \
	yum clean all

# Create oracle directory
RUN mkdir -p /usr/src/oracle
WORKDIR /usr/src/oracle

# Bundle unzipped oracle installer
# COPY . /usr/src/oracle

#RUN yum localinstall -y /usr/src/oracle/Disk1/oracle-xe-11.2.0-1.0.x86_64.rpm
#RUN cd /usr/src/oracle/Disk1
#RUN rpm -ivh oracle-xe-11.2.0-1.0.x86_64.rpm
