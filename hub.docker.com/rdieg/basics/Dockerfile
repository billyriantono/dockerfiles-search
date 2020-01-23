FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install -y software-properties-common

RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update

RUN apt-get install curl make git unzip wget build-essential g++-7 -y

RUN ln -sf /usr/bin/gcc-7 /usr/bin/gcc && ln -sf /usr/bin/g++-7 /usr/bin/g++
RUN g++ --version

COPY include/ /usr/include/
COPY bin/ /usr/bin/
COPY opt/Qt-5.12.0.tar.xz /usr/local/
RUN cd /usr/local && tar -xf Qt-5.12.0.tar.xz
ENV PATH="/usr/local/Qt-5.12.0/bin:${PATH}"
RUN cd /opt
RUN apt-get install -y libssl-dev
RUN wget http://www.cmake.org/files/v3.16/cmake-3.16.0-rc4.tar.gz && tar -xf cmake-3.16.0-rc4.tar.gz
RUN cd cmake-3.16.0-rc4 && ./configure --prefix=/usr && make install
RUN mkdir -p /opt/rdi/cmake
COPY opt/rdi/cmake/ /opt/rdi/cmake