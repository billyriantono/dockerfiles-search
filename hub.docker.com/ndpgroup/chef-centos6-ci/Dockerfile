FROM centos:centos6
MAINTAINER NDP, LLC <http://www.ndpgroup.com>

ARG EL=6
ARG CHANNEL=stable
ARG VERSION=12.5.1

RUN yum -y install centos-release-scl cpio make rsync wget && \
    yum -y install devtoolset-4-toolchain && \
    yum -y update; \
    yum clean all

RUN wget "http://packages.chef.io/files/${CHANNEL}/chef/${VERSION}/el/${EL}/chef-${VERSION}-1.el${EL}.x86_64.rpm" -O /tmp/chef-client.rpm && \
    rpm2cpio /tmp/chef-client.rpm | cpio -idmv && \
    rm -rf /tmp/chef-client.rpm
