FROM centos
MAINTAINER uochan

RUN yum install -y epel-release
RUN yum install -y ansible
RUN yum clean all -y

ADD hosts /etc/ansible/hosts
