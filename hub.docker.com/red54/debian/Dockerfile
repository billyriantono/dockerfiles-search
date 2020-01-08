FROM debian:8
MAINTAINER 谢致邦 <Yeking@Red54.com>
COPY apt /etc/apt
RUN ln -sf /bin/bash /bin/sh \
&& apt-get update && apt-get install -y \
	apt-file \
	automake \
	bison \
	ca-certificates \
	chrpath \
	colordiff \
	cpio \
	deborphan \
	devscripts \
	dnsutils \
	dpkg-dev \
	equivs \
	file \
	flex \
	gawk \
	gccxml \
	git \
	less \
	lib32z1 \
	libfile-fcntllock-perl \
	libncurses5-dev \
	libssl-dev \
	libtool \
	make \
	man-db \
	net-tools \
	openssh-client \
	p7zip \
	proxychains \
	psmisc \
	python \
	quilt \
	sharutils \
	sshfs \
	subversion \
	sudo \
	unzip \
	vim \
	wget \
	xz-utils \
&& apt-file update
