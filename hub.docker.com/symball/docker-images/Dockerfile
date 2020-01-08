FROM ubuntu:bionic

ARG MONGO_C_VERSION=1.12.0
ARG MONGO_CXX_VERSION=3.3.1
ARG ZEROMQ_VERSION=4.3.0
ARG LIBZQ_VERSION=4.2.5
ARG BOOST_VERSION=1.68.1
# Should be the same as boost version replacing the dots for underscores
ARG BOOST_REF=1_68_1

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
  git \
  curl \
  wget \
  vim \
  autoconf \
  automake \
  apt-file \
  build-essential \
  software-properties-common \
  pkg-config \
  python3 \
  libc6-dev \
  libssl-dev \
  libsasl2-dev \
  libtool \
  # Extra introduced to cut out build complexity
  cmake \
  gcc \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

# gcc,g++ 7
# RUN add-apt-repository ppa:ubuntu-toolchain-r/test \
#   && apt-get update && apt-get install -y gcc-7 g++-7 \
#   && apt-get clean && rm -rf /var/lib/apt/lists/* \
#   && rm /usr/bin/gcc /usr/bin/g++ \
#   && ln -s /usr/bin/gcc-7 /usr/bin/gcc \
#   && ln -s /usr/bin/g++-7 /usr/bin/g++

# cmake
# RUN git clone https://gitlab.kitware.com/cmake/cmake.git -b v3.11.1 --depth 1 \
#   && cd cmake \
#   && ./bootstrap --prefix=/usr/local && make -j4 && make install \
#   && cd -

# Boost Driver as prerequisite
WORKDIR /opt
RUN wget https://dl.bintray.com/boostorg/release/${BOOST_VERSION}/source/boost_${BOOST_REF}.tar.gz && \
   tar xvf boost_${BOOST_REF}.tar.gz && \
   cd boost_${BOOST_REF} && \
   ./bootstrap.sh && \
   ./b2 install -j2

# gtest
RUN git clone https://github.com/google/googletest.git -b release-1.8.0 --depth 1 \
 && mkdir -p googletest/_build && cd googletest/_build \
 && cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && make -j4 && make install

# rocksdb
RUN git clone https://github.com/facebook/rocksdb.git -b v5.12.4 --depth 1 \
  && mkdir -p rocksdb/_build && cd rocksdb/_build \
  && cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && make -j4 && make install

# ZeroMQ Driver
WORKDIR /opt
RUN wget https://github.com/zeromq/libzmq/archive/v${LIBZQ_VERSION}.tar.gz && \
  tar xvf v${LIBZQ_VERSION}.tar.gz && \
  mkdir -p libzmq-${LIBZQ_VERSION}/_build && \
  cd libzmq-${LIBZQ_VERSION}/_build && \
  cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
  make && \
  make install

WORKDIR /opt
RUN wget https://github.com/zeromq/cppzmq/archive/v${ZEROMQ_VERSION}.tar.gz && \
  tar xvf v${ZEROMQ_VERSION}.tar.gz && \
  mkdir -p cppzmq-${ZEROMQ_VERSION}/_build && \
  cd cppzmq-${ZEROMQ_VERSION}/_build && \
  cmake -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
  make && \
  make install

# Mongo C Driver as prerequisite
WORKDIR /opt
RUN wget https://github.com/mongodb/mongo-c-driver/archive/${MONGO_C_VERSION}.tar.gz && \
    ls -la && \
    tar xvf ${MONGO_C_VERSION}.tar.gz && \
    cd mongo-c-driver-${MONGO_C_VERSION} && \
    mkdir cmake-build && \
    cd cmake-build && \
    cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && \
    make install


# Mongo C** Driver
WORKDIR /opt
RUN wget https://github.com/mongodb/mongo-cxx-driver/archive/r${MONGO_CXX_VERSION}.tar.gz && \
    tar -xvf r${MONGO_CXX_VERSION}.tar.gz && \
    cd mongo-cxx-driver-r${MONGO_CXX_VERSION}/build && \
    cmake -DBSONCXX_POLY_USE_BOOST=1 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local .. && \
    make && \
    make install

CMD ["/usr/bin/bash"]
