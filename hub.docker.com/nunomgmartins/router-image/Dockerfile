from ubuntu:14.04.4

RUN apt-get update && apt-get install -y \
	git \
	curl \
	build-essential \
	openssh-server \
	diffstat \
	chrpath \
	texinfo \
	gawk \
	vim \
	cscope \
	gdb-multiarch \
	quilt \
	libncurses5-dev \
	ctags

RUN useradd rdkb -ms /bin/bash -p Pze9tec9xh1Qs


RUN curl https://storage.googleapis.com/git-repo-downloads/repo > /bin/repo && chmod a+x /bin/repo

RUN dpkg-reconfigure locales
RUN locale-gen en_US.UTF-8 pt_PT.UTF-8


RUN echo "dash dash/sh boolean false" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

RUN mkdir /var/run/sshd
CMD ["/usr/sbin/sshd", "-D"]
