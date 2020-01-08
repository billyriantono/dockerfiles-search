FROM ubuntu:12.04

MAINTAINER tedwang.tw@gmail.com

#
# fundamental packages
#
RUN apt-get update \
	&& apt-get install -y curl vim git man-db
# optional
RUN apt-get install -y sudo net-tools 

#
# AOSP requirement
#
# host toolchains
RUN apt-get install -y bison g++-multilib gperf libxml2-utils
RUN apt-get install -y gnupg flex build-essential \
	zip libc6-dev libncurses5-dev:i386 x11proto-core-dev \
	libx11-dev:i386 libreadline6-dev:i386 libgl1-mesa-glx:i386 \
	libgl1-mesa-dev mingw32 tofrodos \
	python-markdown xsltproc zlib1g-dev:i386
RUN ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/libGL.so

# Clean up
RUN apt-get clean
