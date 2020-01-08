FROM devops06/centos:7

RUN yum install -y epel-release && yum clean all 
RUN yum install -y ansible && yum clean all 

ENV ANSIBLE_SCP_IF_SSH=y
