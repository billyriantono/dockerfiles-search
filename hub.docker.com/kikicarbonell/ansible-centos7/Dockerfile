FROM centos:7

LABEL maintainer="Enrique Carbonell"

ENV container=docker

RUN curl -o /tmp/epel-release-latest-7.noarch.rpm https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; \
    yum install -y /tmp/epel-release-latest-7.noarch.rpm; rm -rf /tmp/epel-release-latest-7.noarch.rpm

RUN yum install -y git ansible 2.7.8