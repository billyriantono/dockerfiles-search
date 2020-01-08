FROM ubuntu:14.04

MAINTAINER rain <15058553030@163.com>

# install dependencies for compiling hadoop
RUN apt-get update && \
		apt-get install -y wget \
                       openjdk-7-jdk \
                       libprotobuf-dev \
                       protobuf-compiler \
                       maven \
                       cmake \
                       build-essential \
                       pkg-config \
                       libssl-dev \
                       zlib1g-dev \
                       llvm-gcc \
                       automake \
                       autoconf \
                       make

COPY config/* /root/config/

RUN chmod +x /root/config/compile.sh