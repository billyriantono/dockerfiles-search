FROM ubuntu:xenial
ENV VERSION v0.2.0

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN	apt-get install -y \
			libatlas-base-dev \
			libbz2-dev \
			libhdf5-dev \
			liblzma-dev \
			zlib1g-dev \
			make \
			wget \
			bzip2 \
			cmake \
			gcc-4.9 \
			git \
			procps \
			g++

RUN apt-get clean all && \
		apt-get purge && \
		rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


RUN git clone --branch $VERSION https://github.com/rrwick/Filtlong.git && \
	cd Filtlong && \
	make -j

ENV PATH /Filtlong/bin:$PATH
