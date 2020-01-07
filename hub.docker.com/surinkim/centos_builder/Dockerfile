FROM centos:6.8
MAINTAINER Hyunun Kim <nnhope@hotmail.com>

# basic install
RUN yum -y groupinstall "Development Tools" # For g++, make, et. al.
RUN yum -y install wget

# boost 1.55 install
RUN wget --no-check-certificate 'http://sourceforge.net/projects/boost/files/boost/1.55.0/boost_1_55_0.tar.bz2/download'
RUN tar -xvf download
RUN cd boost_1_55_0 && ./bootstrap.sh --without-libraries=python #without python
RUN cd boost_1_55_0 && ./b2 install -s NO_BZIP2=1 #without bzip
RUN rm -rf boost_1_55_0
RUN echo "/usr/local/lib" >> /etc/ld.so.conf
RUN ldconfig

# openssl install
RUN yum -y install openssl-devel

# set workdir
RUN mkdir /src
WORKDIR /src

CMD /bin/bash
