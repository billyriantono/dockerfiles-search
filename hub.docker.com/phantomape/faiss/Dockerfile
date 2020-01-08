FROM nvidia/cuda:10.1-devel

LABEL MAINTAINER="cxucheng@outlook.com"

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /usr/include/
ENV LD_LIBRARY_PATH=/usr/local/lib

RUN apt-get -qq update && apt-get install -qy software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y
RUN apt-get install -qy --fix-missing \ 
    gcc \
    git \
    wget \
    vim \
    g++ \
    libevent-dev \
    libdouble-conversion-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libiberty-dev \
    liblz4-dev \
    liblzma-dev \
    libsnappy-dev \
    make \
    zlib1g-dev \
    binutils-dev \
    libssl-dev \
    pkg-config \
    unzip \
    libunwind8-dev \
    libelf-dev \
    libdwarf-dev \
    libgflags-dev \
    libsnappy-dev \
    zlib1g-dev \
    libbz2-dev \
    liblz4-dev \
    libzstd-dev \
    libsdl2-dev \
    autoconf \
    python3-pip \
    python-pip \
    libnuma-dev \
    curl \
    ninja-build \
    libomp-dev \
    tmux \
    swig

# Build cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v3.13.3/cmake-3.13.3.tar.gz \
    && tar -xzf cmake-3.13.3.tar.gz \
    && rm cmake-3.13.3.tar.gz \
    && cd cmake-3.13.3 \
    && ./bootstrap -- -DCMAKE_BUILD_TYPE:STRING=Release \
    && make -j $(nproc) \
    && make install

RUN pip install numpy

RUN pip3 install numpy

# Build Faiss
# RUN git clone https://github.com/facebookresearch/faiss.git \
#     && cd faiss \
#     && ./configure \
#     && make -j $(nproc) \
#     && make install

ENTRYPOINT /bin/bash
