FROM centos:7.1.1503
MAINTAINER andras.szerdahelyi@gmail.com

# OpsCenter ( web ui; agent RPC )
EXPOSE 8888 61620

ADD etc/yum.repos.d/* /etc/yum.repos.d/

RUN yum -y install opscenter

CMD ["/usr/share/opscenter/bin/opscenter", "-f"]
