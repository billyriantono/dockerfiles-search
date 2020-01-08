FROM ubuntu:18.04

RUN apt-get update
RUN apt-get -y --no-install-recommends install build-essential wget
RUN apt-get -y --no-install-recommends install clang

ENV CC=clang
ENV CXX=clang++

# install cmake boost 1.68.0 requires cmake 3.12.2
RUN wget --no-check-certificate https://cmake.org/files/v3.12/cmake-3.12.2.tar.gz
RUN tar xvf cmake-3.12.2.tar.gz
RUN cd cmake-3.12.2 && ./bootstrap && make && make install

# install boost
RUN wget --no-check-certificate https://dl.bintray.com/boostorg/release/1.68.0/source/boost_1_68_0.tar.gz
RUN tar -xzf boost_1_68_0.tar.gz
RUN cd /boost_1_68_0 && ./bootstrap.sh --with-toolset=clang
RUN cd /boost_1_68_0 && ./b2 install toolset=clang --with=all


