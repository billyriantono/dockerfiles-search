FROM ubuntu:18.04

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install \
	unzip \
	wget \
	git \
	g++ \
	cmake


WORKDIR /opt/
RUN \
	wget -O googletest-release-1.8.1.zip https://github.com/google/googletest/archive/release-1.8.1.zip && \
	unzip googletest-release-1.8.1.zip && \
	rm -rf googletest-release-1.8.1.zip && \
	cd googletest-release-1.8.1 && \
	mkdir build && \
	cd build && \
	cmake .. && \
	make all && \
	make install && \
	cd .. && \
	rm -rf googletest-release-1.8.1


RUN mkdir -p /workspace
WORKDIR /workspace

CMD /bin/bash
