FROM amazonlinux:2017.03.1.20170812

MAINTAINER MooYeol Lee "mooyoul.lee@vingle.net"

# Pin Openssl Version for Lambda runtime comaptiblity
RUN yum localinstall -y http://packages.us-east-1.amazonaws.com/2016.09/updates/15aa5a441a1b/x86_64/Packages/openssl-devel-1.0.1k-15.99.amzn1.x86_64.rpm && \
    yum localinstall -y http://packages.us-east-1.amazonaws.com/2016.09/updates/15aa5a441a1b/x86_64/Packages/openssh-6.6.1p1-33.66.amzn1.x86_64.rpm && \
    yum localinstall -y http://packages.us-east-1.amazonaws.com/2016.09/updates/15aa5a441a1b/x86_64/Packages/openssh-clients-6.6.1p1-33.66.amzn1.x86_64.rpm && \
    yum install -y yum-plugin-versionlock && \
    yum versionlock openssl* openssh* python* && \
    yum clean all

# Prepare build envrionment
RUN yum -y update && \
    yum -y -x openssh* groupinstall "Development Tools" && \
    yum clean all

# Prepare ffmpeg dependencies
RUN yum update -y && \
    yum install -y autoconf automake bzip2 cmake gcc gcc-c++ git libtool make mercurial pkgconfig zlib-devel libcurl-devel && \
    yum clean all
