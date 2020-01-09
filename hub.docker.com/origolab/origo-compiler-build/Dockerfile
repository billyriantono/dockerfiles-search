# Copyright (c) 2018 Origo Foundation
# This file is part of the origo-compiler.
#
# The origo-compiler is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# The origo-compiler is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with the origo. If not, see <http://www.gnu.org/licenses/>.

# The base OS
FROM ubuntu:16.04

MAINTAINER Gavin <g-origo>

LABEL version=0.1

ARG BUILD_JOBS=4
ENV BUILD_JOBS ${BUILD_JOBS}
ENV LLVM_VERSION 6.0.0

RUN apt-get -q -y update && \
    apt-get install --force-yes -q -y \
      automake \
      autoconf \
      binutils-dev \
      cmake \
      curl \
      g++-5 \
      gcc-5 \
      git \
      libgflags-dev \
      libiberty-dev \
      libgoogle-glog-dev \
      libboost-all-dev \
      openssl \
      pkg-config \
      python-pip \
      unzip \
      wget

RUN pip install --upgrade pip
RUN pip install cpplint codecov

# protobuf
RUN cd /opt && \
    wget https://github.com/google/protobuf/archive/v3.6.0.zip && \
    unzip v3.6.0.zip && \
    (cd protobuf-3.6.0 && \
     ./autogen.sh && \
     ./configure && \
     make -j ${BUILD_JOBS}  && \
     make install && \
     ldconfig) && \
    rm -rf v3.6.0.zip protobuf-3.6.0

# gtest
RUN cd /opt && \
    wget https://github.com/google/googletest/archive/release-1.8.0.zip && \
    unzip release-1.8.0.zip && \
    (cd googletest-release-1.8.0 && \
     mkdir build && \
     cd build && \
     cmake -DBUILD_SHARED_LIBS=ON .. && \
     make -j ${BUILD_JOBS}  && \
     make install && \
     ldconfig) && \
    rm -rf release-1.8.0.zip googletest-release-1.8.0

# llvm
RUN rm -rf /var/lib/apt/lists/* && \
    wget -O - http://llvm.org/releases/${LLVM_VERSION}/clang+llvm-${LLVM_VERSION}-x86_64-linux-gnu-ubuntu-16.04.tar.xz \
    | tar xJf - --strip-components 1 -C /usr/local/ clang+llvm-${LLVM_VERSION}-x86_64-linux-gnu-ubuntu-16.04