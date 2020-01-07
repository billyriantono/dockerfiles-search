FROM ubuntu:14.04
MAINTAINER Evgeny Timoshenko <evgeny.timoshenko@rubius.com>
RUN apt-get update -y && \
	apt-get install --no-install-recommends -y -q \
		build-essential python2.7 python2.7-dev python-pip
RUN apt-get install -y \
	python-numpy \
	python-scipy \
	python-matplotlib \
	ipython ipython-notebook \
	python-pandas \
	python-sympy \
	python-nose

RUN apt-get install -y python-skimage

RUN apt-get install -y python-opencv
RUN pip install -U pip

