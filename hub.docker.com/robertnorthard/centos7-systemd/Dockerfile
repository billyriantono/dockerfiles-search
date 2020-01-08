# Defines Docker image suitable for testing cookbooks on CentOS 7.
FROM centos:centos7

MAINTAINER Robert, Northard

RUN yum clean all && \ 
    yum -y swap — remove fakesystemd — install systemd systemd-libs && \ 
  yum -y install openssh-server openssh-clients initscripts && \ 
  systemctl enable sshd.service 
