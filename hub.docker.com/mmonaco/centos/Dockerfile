FROM centos:7
MAINTAINER Matthew Monaco <matt@monaco.cx>
ENV LANG=en_US.UTF-8
ENV TERM=xterm

# Enable docs for manpages
RUN sed '/^tsflags=/d' -i /etc/yum.conf

RUN yum -y makecache \
 && yum -y install epel-release \
 && yum -y upgrade \
 && yum -y autoremove \
 && yum -y clean all

RUN yum -y install \
	bash-completion \
	bind-utils \
	git \
	iproute \
	locales \
	man \
	net-tools \
	procps-ng \
	tcpdump \
	tree \
	vim-enhanced \
	whois \
 && yum -y clean all

# systemd

ENV container docker
RUN rm -f \
	/lib/systemd/system/multi-user.target.wants/* \
	/lib/systemd/system/local-fs.target.wants/* \
	/lib/systemd/system/sockets.target.wants/*udev* \
	/lib/systemd/system/sockets.target.wants/*initctl* \
	/lib/systemd/system/basic.target.wants/* \
	/lib/systemd/system/anaconda.target.wants/* \
	/etc/systemd/system/*.wants/* \
 && (cd /lib/systemd/system/sysinit.target.wants ; for i in *; do [ "$i" == systemd-tmpfiles-setup.service ] || rm -f "$i"; done)

VOLUME /sys/fs/cgroup

# debugging

ADD bashrc /root/.bashrc
WORKDIR /root
