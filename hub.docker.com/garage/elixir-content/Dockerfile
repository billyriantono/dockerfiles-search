FROM ubuntu:14.04

# maintainer
MAINTAINER Krutika Gaonkar

RUN apt-get update && apt-get install -y \
	autoconf \
	automake \
	make \
	g++ \
	gcc \
	build-essential \ 
	zlib1g-dev \
	libgsl0-dev \
	perl \
	python \
	curl \
	git \
	wget \
	unzip \
	tabix \
	libncurses5-dev


WORKDIR /opt
RUN git clone https://github.com/parklab/NGSCheckMate.git
RUN export NCM_HOME=/opt/NGSCheckMate
RUN cd $NCM_HOME





 



