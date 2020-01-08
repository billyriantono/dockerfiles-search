FROM ubuntu:16.04

MAINTAINER Michael Dong <michael.dong@vrviu.com>
RUN sed -i 's/archive.ubuntu/mirrors.163/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		wget \
		vim \
		net-tools \
		iputils-ping \
		bzr \
		git \
		psmisc \
		mercurial \
		openssh-client \
		subversion \
		procps \
		telnet \
		subversion \
		libcurl4-nss-dev \
		gnupg2 \
		dirmngr \
		bzip2 \
		unzip \
		xz-utils \
		openssh-server \
		cron \
		tzdata \
	&& rm -rf /var/lib/apt/lists/* \
	&& sed -i 's/^PermitRootLogin .*/PermitRootLogin yes/' /etc/ssh/sshd_config \
	&& rm -rf /etc/update-motd.d/10-help-text \
	&& echo root:e7SfdwhEztkv0T55|chpasswd

RUN ln -fs /usr/share/zoneinfo/Asia/Harbin /etc/localtime && dpkg-reconfigure -f noninteractive tzdata
ENV LANG C.UTF-8

CMD ["/bin/bash"]
