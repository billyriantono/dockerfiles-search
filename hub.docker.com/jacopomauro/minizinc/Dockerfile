FROM debian:stretch
MAINTAINER Jacopo Mauro

RUN apt-get update &&\
	apt-get -y install \
		git \
		wget \
		libgl1 && \
	rm -rf /var/lib/apt/lists/* && \
	mkdir /tool && \
	cd /tool && \
	wget https://github.com/MiniZinc/MiniZincIDE/releases/download/2.3.1/MiniZincIDE-2.3.1-bundle-linux-x86_64.tgz && \
	tar -zxvf MiniZincIDE-2.3.1-bundle-linux-x86_64.tgz && \
	mv /tool/MiniZincIDE-2.3.1-bundle-linux /tool/MiniZincIDE && \
	rm -rf MiniZincIDE-2.3.1-bundle-linux-x86_64.tgz
	
ENV PATH "$PATH:/tool/MiniZincIDE/bin"
ENV LD_LIBRARY_PATH "$LD_LIBRARY_PATH:/tool/MiniZincIDE/lib"

