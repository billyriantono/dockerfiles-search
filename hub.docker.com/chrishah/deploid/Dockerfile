FROM ubuntu:18.04

RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential vim git wget \
	autoconf autoconf-archive libcppunit-dev zlib1g-dev

WORKDIR /usr/src
RUN git clone --recursive https://github.com/mcveanlab/DEploid.git && \
	cd DEploid && \
	git reset --soft ad64adde1de3924b268fabde03b09845d288bb35 && \
	./bootstrap && \
	make
ENV PATH=$(PATH):/usr/src/DEploid
