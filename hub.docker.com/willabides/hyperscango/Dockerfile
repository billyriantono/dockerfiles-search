FROM debian:jessie

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
  build-essential \
  pkg-config \
  cmake \
  libboost-all-dev \
  ragel \
  lsb-release \
  curl \
  git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /tmp

RUN \
  set -x -v && \
  curl -L -O https://dl.bintray.com/boostorg/release/1.65.1/source/boost_1_65_1.tar.gz && \
  shasum -a256 boost_1_65_1.tar.gz | grep a13de2c8fbad635e6ba9c8f8714a0e6b4264b60a29b964b940a22554705b6b60 && \
  tar -C /usr/local -xzf boost_1_65_1.tar.gz

RUN \
  set -x -v && \
  curl -L -O https://github.com/intel/hyperscan/archive/v4.7.0.tar.gz && \
  tar -xf v4.7.0.tar.gz && \
  cd hyperscan-4.7.0 && \
  cmake -DCMAKE_BUILD_TYPE=Release -DBOOST_ROOT=/usr/local/boost_1_65_1 . && \
  make && \
  make install

RUN \
  set -x -v && \
  curl -L -O https://dl.google.com/go/go1.11.linux-amd64.tar.gz && \
  shasum -a256 go1.11.linux-amd64.tar.gz | grep b3fcf280ff86558e0559e185b601c9eade0fd24c900b4c63cd14d1d38613e499 && \
  tar -C /usr/local -xzf go1.11.linux-amd64.tar.gz
