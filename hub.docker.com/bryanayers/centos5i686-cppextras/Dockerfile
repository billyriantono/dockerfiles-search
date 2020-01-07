# Base OS
FROM incendonet/centos5i686
MAINTAINER info@incendonet.com

# Env setup
ENV HOME /root
WORKDIR ~/

# Build deps
RUN \
	yum -y update && \
	yum -y install alsa-lib-devel.i386 e2fsprogs-devel.i386 gcc44.x86_64 gcc-c++.x86_64 glibc-devel.i386 postgresql.i686
