#
# Cent OS 6 configured for Japan Standard Time
#
FROM centos:centos6
MAINTAINER sokutou-metsu sktmt

ENV LANG en_US.UTF-8

# Configures Time Zone
RUN yum -y update &&\
    yum -y install ntp &&\
    yum -y clean all
RUN echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock
RUN rm -f /etc/localtime &&\
    ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime &&\
    ntpdate ntp.nict.jp

ENTRYPOINT ["/bin/bash", "-c"]
