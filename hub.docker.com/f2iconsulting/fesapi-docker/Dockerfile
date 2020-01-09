# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"; you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
# http://www.apache.org/licenses/LICENSE-2.0
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

FROM centos:6.8

LABEL maintainer="philippe.verney@f2i-consulting.com"

RUN yum update -y \
	&& yum install -y \
	zlib-devel \
	automake \
	pcre-devel \
	git \
	gcc \
	gcc-c++ \
	make \
	byacc \
	java-1.8.0-openjdk-devel \
	libuuid-devel

WORKDIR fesapiEnv

#ENV MAKE_OPTS=-j

ENV CFLAGS="-DNOCRYPT -fPIC -O2"
ENV CXXFLAGS="-DNOCRYPT -fPIC -O2"

WORKDIR /fesapiEnv/dependencies
ENV FES_INSTALL_DIR=/fesapiEnv/dependencies/install
RUN mkdir -p $FES_INSTALL_DIR
ENV PATH=$FES_INSTALL_DIR/bin:$PATH

#ADD cmake-3.14.1-Linux-x86_64.tar.gz
WORKDIR /fesapiEnv/dependencies
ADD https://github.com/Kitware/CMake/releases/download/v3.14.1/cmake-3.14.1-Linux-x86_64.tar.gz .
RUN tar xf cmake-3.14.1-Linux-x86_64.tar.gz
ENV PATH=/fesapiEnv/dependencies/cmake-3.14.1-Linux-x86_64/bin:$PATH

# Minizip
WORKDIR /fesapiEnv/dependencies
RUN git clone https://github.com/F2I-Consulting/Minizip.git
WORKDIR Minizip/build
RUN cmake ../
RUN make
RUN make install

# HDF5
WORKDIR /fesapiEnv/dependencies
#ADD hdf5-1.8.21.tar.gz .
ADD https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.8/hdf5-1.8.21/src/hdf5-1.8.21.tar.gz .
RUN tar xf hdf5-1.8.21.tar.gz
WORKDIR hdf5-1.8.21
RUN ./configure --enable-static=yes --enable-shared=false --prefix=$FES_INSTALL_DIR
RUN make VERBOSE=ON $MAKE_OPTS
RUN make install

# swig
WORKDIR /fesapiEnv/dependencies
RUN git clone https://github.com/swig/swig.git
WORKDIR swig
RUN git checkout tags/rel-3.0.12
RUN ./autogen.sh
RUN ./configure --prefix=$FES_INSTALL_DIR
RUN make $MAKE_OPTS
RUN make install

# Fesapi
WORKDIR /fesapiEnv
RUN git clone https://github.com/F2I-Consulting/fesapi.git
WORKDIR fesapi
#RUN git checkout tags/v0.14.0.0

WORKDIR /fesapiEnv/build
RUN cmake \
 	-DHDF5_C_INCLUDE_DIR=$FES_INSTALL_DIR/include \
 	-DHDF5_C_LIBRARY_RELEASE=$FES_INSTALL_DIR/lib/libhdf5.a \
	-DMINIZIP_INCLUDE_DIR=../dependencies/Minizip/build/install/include \
	-DMINIZIP_LIBRARY_RELEASE=../dependencies/Minizip/build/install/lib/libminizip.a \
 	-DZLIB_INCLUDE_DIR=/usr/include \
 	-DZLIB_LIBRARY_RELEASE=/usr/lib64/libz.so \
 	-DUUID_INCLUDE_DIR=/usr/include \
 	-DUUID_LIBRARY_RELEASE=/lib64/libuuid.so.1 \
	-DWITH_JAVA_WRAPPING=ON \
	-DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_C_FLAGS="" \
	-DCMAKE_CXX_FLAGS="" \
	-DCMAKE_CXX_FLAGS_RELEASE="-O1 -DNDEBUG" \
	-DCMAKE_C_FLAGS_RELEASE="-O1 -DNDEBUG" \
 	../fesapi

#RUN make VERBOSE=ON $MAKE_OPTS FesapiCpp
RUN make VERBOSE=ON $MAKE_OPTS
RUN make install
RUN tar cfz libFesapiCpp.tar.gz install
