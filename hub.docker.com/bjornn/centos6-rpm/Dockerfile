FROM centos:6
RUN yum install -y epel-release
RUN yum groupinstall -y 'Development Tools'
RUN yum install -y wget rpmdevtools yum-utils
RUN useradd builder

USER builder
WORKDIR /home/builder/
RUN rpmdev-setuptree

USER root