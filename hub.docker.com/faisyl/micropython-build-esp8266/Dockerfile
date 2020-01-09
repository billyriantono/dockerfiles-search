FROM ubuntu:14.04

MAINTAINER <faisal.is@gmail.com>

ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV TERM=xterm
ENV CT_ALLOW_BUILD_AS_ROOT_SURE=1

RUN echo "force-unsafe-io" > /etc/dpkg/dpkg.cfg.d/02apt-speedup

RUN apt-get update && apt-get install -qyy  make unrar-free autoconf automake \
	libtool gcc g++ gperf flex bison texinfo gawk \
	ncurses-dev libexpat-dev python-dev python \
	python-serial sed git unzip bash help2man wget \
	bzip2 libtool && \
	apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN cd / && git clone --recursive https://github.com/pfalcon/esp-open-sdk.git 
RUN cd esp-open-sdk && make && rm /esp-open-sdk/*zip && rm -rf /esp-open-sdk/crosstool-NG/.build
ENV PATH=/esp-open-sdk/xtensa-lx106-elf/bin:$PATH



