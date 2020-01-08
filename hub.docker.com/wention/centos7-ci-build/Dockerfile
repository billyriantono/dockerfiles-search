FROM centos:7
MAINTAINER wention xuyi.828@gmail.com

# build tools
RUN yum install -y make git gcc rpm-build rpm-utils autoconf automake patch

# packing tools
RUN yum install -y \
            genisoimage \
            createrepo \
            unzip \
            syslinux \
            pycrypto \
            openssl
