FROM ubuntu:18.04

LABEL maintainer="Data Machines Corp.<help@datamachines.io>"
LABEL protoc_version="3.5.1"
LABEL grpc_version="1.12.0"
LABEL language="c++:11"

ENV LANG en_US.UTF-8
ENV PROTOC_VERSION 3.5.1
ENV GRPC_VERSION 1.12.0

RUN apt-get update && apt-get install -y \
  build-essential autoconf libtool git pkg-config curl \
  automake libtool curl make g++ unzip \
  && apt-get clean

# install protobuf first, then grpc
ENV GRPC_RELEASE_TAG v1.12.x
RUN git clone -b ${GRPC_RELEASE_TAG} https://github.com/grpc/grpc /var/local/git/grpc && \
		cd /var/local/git/grpc && \
    git submodule update --init && \
    echo "--- installing protobuf ---" && \
    cd third_party/protobuf && \
    ./autogen.sh && ./configure --enable-shared && \
    make -j$(nproc) && make -j$(nproc) check && make install && make clean && ldconfig && \
    echo "--- installing grpc ---" && \
    cd /var/local/git/grpc && \
    make -j$(nproc) && make install && make clean && ldconfig
