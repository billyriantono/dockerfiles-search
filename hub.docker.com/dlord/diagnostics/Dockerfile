FROM centos:centos7

RUN yum install -y epel-release \
    && yum install -y \
        net-tools \
        bind-utils \
        tcpdump \
        telnet \
        traceroute \
        nmap-ncat \
        wireshark \
    && yum clean all -y; \
    rm -rf /var/cache/yum/* /tmp/*
