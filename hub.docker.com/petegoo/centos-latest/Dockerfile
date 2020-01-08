FROM centos:latest

MAINTAINER Peter Goodman <docker@petegoo.com>

# Enable non-interactive installation by yum and update
RUN sed -i 's/^\[main\]/\[main\]\nassumeyes = 1/' /etc/yum.conf && \
    yum update && yum clean all