FROM nathankw/centos6_essentials
LABEL maintainer "Nathaniel Watson nathankw@stanford.edu"

#Folders /srv/src and /srv/software were created in the base image.

#INSTALL Python 2.7.14 along with scipy and numpy packages.
RUN curl -O https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz \
	&& tar -zxf Python-2.7.14.tgz \
	&& rm Python-2.7.14.tgz \
	&& cd Python-2.7.14 \
	&& ./configure \
	&& make \
	&& make install \
	&& curl -O https://bootstrap.pypa.io/get-pip.py \
	&& python get-pip.py \
  && pip install numpy \
  && pip install scipy
