FROM ubuntu:xenial

RUN apt-get update && apt-get install -yq \
    sudo \
    git \
    cmake \
    g++ \
    flex \
    bison \
    libkrb5-dev \
    libsasl2-dev \
    libnuma-dev \
    pkg-config \
    libssl-dev \
    libcap-dev \
    gperf \
    autoconf-archive \
    libevent-dev \
    libtool \
    libboost-all-dev \
    libjemalloc-dev \
    libsnappy-dev \
    wget \
    \
    google-mock \
    libgoogle-glog0v5 \
    libgtest-dev \
    \
    libgoogle-glog-dev \
    libgflags-dev \
    libdouble-conversion-dev \
    rubygems ruby-dev

#TODO: above package rubygems, ruby-dev and below gem fpm is used to package debian packages, which should be one dind layer above

RUN gem install fpm

CMD ["/bin/bash"]
