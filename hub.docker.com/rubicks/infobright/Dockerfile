# github.com/rubicks/dockers/infobright/Dockerfile

FROM centos:6.6

MAINTAINER rubicks

RUN \
  yum -y update && \
  yum -y upgrade && \
  yum -y install wget sudo openssh-clients && \
  >>/etc/sudoers echo "Defaults !requiretty" && \
  wget -nv -O infobright-4.0.7-0-x86_64-ice.rpm \
    http://www.infobright.org/downloads/ice/infobright-4.0.7-0-x86_64-ice.rpm && \
  yum -y localinstall infobright-4.0.7-0-x86_64-ice.rpm

