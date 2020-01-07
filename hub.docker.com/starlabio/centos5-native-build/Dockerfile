FROM astj/centos5-vault
MAINTAINER Greg Pearson <greg.pearson@starlab.io>

RUN yum update -y && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*

# Install EPEL
RUN yum install -y epel-release && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*

# Install development tools
RUN yum groupinstall -y "development tools" && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*

# Install git (requires epel-release)
RUN yum install -y git && \
    yum clean all && \
    rm -rf /var/cache/yum/* /tmp/* /var/tmp/*
