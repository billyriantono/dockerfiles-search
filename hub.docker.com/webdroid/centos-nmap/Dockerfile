FROM centos:latest
MAINTAINER Webdroid

RUN yum -y update \
&& yum -y install nmap \
&& yum clean all \
&& mkdir /workdir

VOLUME /workdir
WORKDIR /workdir

ENTRYPOINT ["nmap"]
