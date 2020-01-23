#
#  Dockerfile for a GPDB Base Image - MASTER Node
#  greenplum-db-4.3.7.2-build-2-RHEL5-x86_64

FROM centos:7
MAINTAINER david.harris@bramhalldata.com

COPY * /tmp/

RUN echo root:pivotal | chpasswd \
	&& yum install -y unzip which more ed wget openssh-clients openssh-server ntp; yum clean all \
	&& wget http://bit.ly/1WSiZIm -P /tmp/ \
	&& unzip /tmp/1WSiZIm -d /tmp/ \
	&& rm /tmp/1WSiZIm \
	&& sed -i s/"more << EOF"/"cat << EOF"/g /tmp/*.bin \	
	&& echo -e "yes\n/data/greenplum\nyes\nyes\n" | /tmp/*.bin \
	&& rm -f /tmp/*.bin \	
	&& cat /tmp/sysctl.conf.add >> /etc/sysctl.conf \
        && cat /tmp/limits.conf.add >> /etc/security/limits.conf \
	&& rm -f /tmp/*.add
     

EXPOSE 5432 22

VOLUME /gpdata
