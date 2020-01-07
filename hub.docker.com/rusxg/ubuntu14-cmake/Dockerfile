FROM ubuntu:14.04

RUN \
	apt-get update && \
	apt-get install wget build-essential -y && \
	wget https://cmake.org/files/v3.7/cmake-3.7.1.tar.gz && \
	tar xvf cmake-3.7.1.tar.gz && \
	cd cmake-3.7.1 && \
	./configure && \
	make && \
	make install && \
	cd .. && rm -rf cmake-3.7.1 && \
        rm cmake-3.7.1.tar.gz && \
	apt-get -y clean all && \
	rm -rf /var/lib/apt/lists/*


