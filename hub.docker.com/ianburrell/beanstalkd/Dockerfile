FROM centos:7

MAINTAINER Ian Burrell <ianburrell@gmail.com>

RUN yum install -y epel-release
RUN yum install -y beanstalkd

ENTRYPOINT /usr/bin/beanstalkd
