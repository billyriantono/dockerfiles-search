FROM centos:7

RUN \
  yum update -y && \
  yum install -y epel-release && \
  yum install -y python-setuptools inotify-tools && \
  yum install -y java-1.8.0-openjdk && \
  yum clean all && \
  easy_install supervisor
