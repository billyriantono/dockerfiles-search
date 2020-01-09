FROM centos:6.8
MAINTAINER AooJ <aooj@n13.cz>

ENV GLIBC_VERSION=2.16.0

RUN     yum -y install wget gcc make && \
	mkdir -p /tmp/glibc/build && \
	cd /tmp/glibc && \
	wget http://ftp.gnu.org/gnu/glibc/glibc-${GLIBC_VERSION}.tar.gz && \
	tar zxvf glibc-${GLIBC_VERSION}.tar.gz && \
	cd /tmp/glibc/build && \
	/tmp/glibc/glibc-${GLIBC_VERSION}/configure --prefix=/opt/glibc-${GLIBC_VERSION} && \
	make -j4


VOLUME /tmp/glibc/build

