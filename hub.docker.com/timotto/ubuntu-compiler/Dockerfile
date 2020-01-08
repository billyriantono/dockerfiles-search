FROM ubuntu:14.04

RUN apt-get update && apt-get install -y \
	gcc g++ make autoconf automake \
	libncurses5-dev gawk flex bison \
	texinfo wget gettext python-setuptools \
	python-dev patch git curl xz-utils fakeroot debhelper \
	bc libssl-dev \
	&& rm -rf /var/cache/apt/archives/*

