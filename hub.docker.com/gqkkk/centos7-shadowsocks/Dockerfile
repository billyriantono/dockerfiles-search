# shadowsocks 
# 
# VERSION 0.0.1 
FROM centos 
MAINTAINER gqkkk <guoqing1977@gmail.com> 
RUN yum -y update && \
    yum -y install epel-release && \
    yum clean all && \
    yum -y install python-pip && \
    yum clean all && \
    pip install shadowsocks==2.8.2
# Configure container to run as an executable 
ENTRYPOINT ["/usr/bin/ssserver"]
