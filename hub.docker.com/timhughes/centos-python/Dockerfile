FROM centos:7
RUN yum -y install \
	curl \
	gcc \
	gcc-c++ \
	libyaml-devel \
	libffi-devel \
	make \
	openssl-devel \
	patch \
	readline-devel \
	zlib-devel \
    autoconf \
    automake \
    bzip2 \
    bzip2-devel \
    file \
    gcc \
    gcc-c++ \
    git \
    hostname \
    ncurses-devel  \
    patch \
    readline-devel  \
    rpmdevtools \
    snappy-devel \
    sqlite-devel \
    tar \
    wget \
    xz

RUN	yum clean all

RUN git clone git://github.com/yyuu/pyenv.git /tmp/pyenv
RUN cd /tmp/pyenv/plugins/python-build && sh install.sh
RUN rm -rf /tmp/pyenv
RUN python-build 3.7.4 /usr/local/python

ENV PATH /usr/local/python/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
