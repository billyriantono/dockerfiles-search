FROM centos:7
MAINTAINER zhfang zhfang@dataman-inc.com

ENV TERM=xterm

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && yum install -y vim wget telnet net-tools \
    && yum clean all \
    && rm -rf /var/cache/yum/*
    
