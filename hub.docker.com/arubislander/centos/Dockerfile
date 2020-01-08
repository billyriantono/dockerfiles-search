# This image sets up a CentOS 6.x container for 32bit development
FROM centos:6
MAINTAINER ArubIslander <arubislander@zonnet.nl>

RUN yum install -y \
   automake \
   gcc \
   gcc-c++ \
   glibc-devel.i686 \
   libgcc.i686 \
   libstdc++.i686 \
   make \
   nano \
&& yum clean headers packages metadata
