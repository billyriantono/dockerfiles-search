###################################
# Dockerfile for c++7 image proce-#
#  ssing in Linux environment     #
# BigDataEurope, Horizon2020      #
#                                 #
# ubuntu:16.04                    #
# git 1.9.1                       #
# tomcat 8.0.23                   #
# vim                             #
###################################


FROM ubuntu:16.04

MAINTAINER Giorgos Argyriou <gioargyr@gmail.com>

# INSTALL PREREQUISITIES
RUN apt-get update \
 && apt-get install -y \
    wget \
    curl \
    git \
    vim \
    unzip \
    software-properties-common \
    python-pip \
    libproj-dev \
    libboost-all-dev \
    libxml2-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/

## INSTALLATION OF c++7
RUN add-apt-repository ppa:jonathonf/gcc-7.2 -y \
 && apt-get update \
 && apt-get install -y gcc-7 g++-7

### INSTALLATION OF cmake 3.9.4
#RUN wget --directory-prefix=/downloads https://cmake.org/files/v3.9/cmake-3.9.4.tar.gz \
# && cd /downloads \
# && tar -xzvf cmake-3.9.4.tar.gz \
# && cd /downloads/cmake-3.9.4 \
# && ./bootstrap \
# && make -j4 \
# && make install

### INSTALLATION OF gdal 2.2.2
#RUN wget --directory-prefix=/downloads http://download.osgeo.org/gdal/2.2.2/gdal-2.2.2.tar.gz \
# && cd /downloads \
# && tar -xzvf gdal-2.2.2.tar.gz \
# && cd /downloads/gdal-2.2.2 \
# && ./configure CC=/usr/bin/gcc-7 CXX=/usr/bin/g++-7 \
# && make -j4 \
# && make install
## && cp /usr/local/lib/libgdal.so.20 /usr/lib/

### INSTALLATION OF PROCESSING/DOWNLOADING executables
## elevation python module for downloading dems
#RUN pip install elevation

#RUN cp /usr/local/lib/libgdal.so.20 /usr/lib/ \
# && gdalinfo --version \
# && eio selfcheck \
# && rm -rf /downloads/*
