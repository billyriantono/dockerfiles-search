FROM ubuntu:14.04

MAINTAINER Krutika Gaonkar (gaonkark@email.chop.edu)

# maintainer
MAINTAINER Krutika Gaonkar

RUN apt-get update && apt-get install -y \
	autoconf \
	automake \
	python2.7 \
	python-pip \
	make \
	g++ \
	gcc \
	build-essential \ 
	zlib1g-dev \
	libgsl0-dev \
	perl \
	curl \
	git \
	wget \
	unzip \
	tabix \
	bzip2 \
	libncurses5-dev

WORKDIR /opt
RUN wget https://github.com/Illumina/manta/releases/download/v1.5.0/manta-1.5.0.centos6_x86_64.tar.bz2 
RUN tar -jxvf manta-1.5.0.centos6_x86_64.tar.bz2
WORKDIR /opt/manta-1.5.0.centos6_x86_64 
