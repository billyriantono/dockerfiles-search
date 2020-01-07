FROM centos:centos7
MAINTAINER Kevin Coakley <kcoakley@sdsc.edu>

RUN yum -y install epel-release && \
    yum -y install ansible && \
    yum clean all
RUN echo -e '[local]\nlocalhost' > /etc/ansible/hosts