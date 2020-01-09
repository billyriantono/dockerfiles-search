FROM centos:7.2.1511
MAINTAINER pigyang <372282766.qq.com>

ADD init.sh /init.sh

RUN chmod a+x /init.sh
RUN /bin/bash init.sh
RUN rm -rf /init.sh
RUN mkdir -p /xy
RUN yum install --downloadonly --downloaddir=/xy kubelet kubeadm -y
