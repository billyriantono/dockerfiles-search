FROM centos:7

# for JAPAN 
RUN ln -sf /usr/share/zoneinfo/Japan /etc/localtime
RUN echo "include_only=.jp" >> /etc/yum/pluginconf.d/fastestmirror.conf

RUN yum -y update; yum clean all
