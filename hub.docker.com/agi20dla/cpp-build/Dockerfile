FROM ubuntu:trusty
MAINTAINER Jason C. Sherman <agi20dla@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV CMAKE_CXX_COMPILER /usr/bin/g++

RUN apt-get update \
&& apt-get -y install \
    make \
    automake \
    git \
    curl \
    libboost1.55-all-dev \
    g++ \
    cpputest \
    google-mock \
    vim \
&& rm -rf /var/lib/apt/lists/*

# build cmake
RUN curl -O https://cmake.org/files/v3.4/cmake-3.4.3.tar.gz \
    && tar -xvf cmake-3.4.3.tar.gz
WORKDIR cmake-3.4.3
RUN ./bootstrap \
    && make \
    && make install

# install gmock
#RUN git clone https://github.com/google/googletest.git
#WORKDIR googletest
#RUN mkdir build
#WORKDIR build
#RUN cmake .. && make && make install

ENTRYPOINT /bin/bash


