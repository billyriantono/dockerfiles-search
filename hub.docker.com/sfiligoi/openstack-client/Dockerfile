FROM centos:centos7

RUN yum update -y

RUN yum -y install epel-release
RUN yum -y install centos-release-openstack-stein
RUN yum -y install python2-openstackclient

RUN yum update -y

RUN yum clean all

# This container will sleep forever
# The idea being that one gets into it by some other mean
CMD ["/bin/sh" ,"-c" ,"sleep infinity"]
