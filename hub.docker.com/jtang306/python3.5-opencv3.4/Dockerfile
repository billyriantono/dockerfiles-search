FROM ubuntu:16.04
MAINTAINER VCA Technology <developers@vcatechnology.com>

#update all packages
RUN apt-get update \
  && apt-get -y dist-upgrade \
  && apt-get -y install build-essential \  
  && apt-get -y install locales \
  && apt-get -y install libssl-dev openssl \
  && apt-get -y install libgtk2.0-dev \
  && apt-get -y install wget \
  && apt-get -y autoremove \
  && apt-get clean 

#Export env settings
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN wget https://www.python.org/ftp/python/3.5.5/Python-3.5.5.tgz \
  && tar xzvf Python-3.5.5.tgz \
  && cd Python-3.5.5 \
  && ./configure \
  && make \
  && make install
RUN pip3 install --upgrade pip \
  && pip3 install pillow \
  && pip3 install opencv-python

