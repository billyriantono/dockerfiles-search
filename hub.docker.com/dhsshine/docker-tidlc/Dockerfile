FROM ubuntu:16.04

RUN \
  apt-get update \
  && apt-get install -y \
  git \
  flex \
  bison \
  libgtest-dev \
  libperl-dev \
  libgtk2.0-dev \
  build-essential \
  cmake \
  && rm -rf /var/lib/apt/lists/*
  
RUN \
  cd /usr/src/gtest \
  && cmake CMakeLists.txt \
  && make \
  && cp ./*.a /usr/lib/
RUN \
  git clone https://git.tizen.org/cgit/platform/core/appfw/tidl -b tizen \
  && cd tidl \
  && ./build.sh build \
  && cp ./build/idlc/tidlc /usr/local/bin/tidlc
