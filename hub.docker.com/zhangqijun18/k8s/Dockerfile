FROM centos
COPY kibana.repo /etc/yum.repos.d/
RUN yum -y install wget
RUN yum repolist
RUN yum -y install --downloaddir=. --downloadonly kibana-6.8.4

