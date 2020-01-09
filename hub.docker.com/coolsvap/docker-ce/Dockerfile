FROM centos:7
MAINTAINER Swapnil Kulkarni "me@coolsvap.net"

RUN yum install -y yum-utils &&\
  yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

ENV DOWNLOAD_DIR /data
CMD yum install --downloadonly --downloaddir=${DOWNLOAD_DIR} docker-ce
