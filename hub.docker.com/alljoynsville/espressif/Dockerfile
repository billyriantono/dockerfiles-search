FROM alljoynsville/build-essential

ENV DEBIAN_FRONTEND noninteractive
USER root
RUN apt-get -yqq update && \
	apt-get -yqq install unrar-free autoconf automake libtool gcc g++ gperf \
			flex bison texinfo gawk ncurses-dev libexpat-dev python-dev python python-serial \
			sed unzip help2man bzip2  \
			&& \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "builder ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR  /builder
USER builder

RUN git clone --recursive https://github.com/pfalcon/esp-open-sdk.git && cd esp-open-sdk && make && \
	echo 'export PATH=/builder/esp-open-sdk/xtensa-lx106-elf/bin:$PATH' >> .bashrc
