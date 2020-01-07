FROM nathankw/centos6_essentials
LABEL maintainer "Nathaniel Watson nathankw@stanford.edu"

#Folders /srv/src and /srv/software were created in the base image.

#INSTALL Python 3.6.4 along with scipy and numpy packages.
RUN curl -O https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz \
	&& tar -zxf Python-3.6.4.tgz \
	&& rm Python-3.6.4.tgz \
	&& cd Python-3.6.4 \
	&& ./configure \
	&& make \
	&& make install 
#comes with pip3.
