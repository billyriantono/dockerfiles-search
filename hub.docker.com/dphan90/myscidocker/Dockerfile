FROM ubuntu:16.04

# Initialize Ubuntu enviroment
RUN apt-get update
MAINTAINER DungPhan <brianp.dung@utexas.edu>
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -y upgrade

# ROOT pre-requisite
RUN apt-get install -y git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev wget curl libtbb2

RUN apt-get install -y gfortran libssl-dev libpcre3-dev xlibmesa-glu-dev libglew1.5-dev libftgl-dev libmysqlclient-dev libfftw3-dev libcfitsio-dev graphviz-dev libavahi-compat-libdnssd-dev libldap2-dev python-dev libxml2-dev libkrb5-dev libgsl0-dev libqt4-dev

# Installing ROOT
RUN mkdir -p /home/dphan/ROOT/
WORKDIR /home/dphan/ROOT/
RUN wget https://root.cern.ch/download/root_v6.14.06.Linux-ubuntu16-x86_64-gcc5.4.tar.gz
RUN tar -xvzf root_v6.14.06.Linux-ubuntu16-x86_64-gcc5.4.tar.gz
RUN mkdir -p /home/dphan/Workspace/
WORKDIR /home/dphan/Workspace/
