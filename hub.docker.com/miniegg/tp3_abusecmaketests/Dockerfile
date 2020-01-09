FROM ubuntu:16.04

ADD . /opt/build/abuse/

WORKDIR /opt/build/abuse

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository ppa:ubuntu-toolchain-r/test \
    && apt-get update \
    && apt-get install -y \
         apt-utils \
         autoconf \
         build-essential \
         file \
         g++-8 \
         make \
         libcurl3 \
         kcov \
         wget \
      && rm -rf /var/lib/apt/lists/* \
      && wget https://cmake.org/files/v3.12/cmake-3.12.1-Linux-x86_64.sh \
      && sh cmake-3.12.1-Linux-x86_64.sh --skip-license --prefix=/usr/local/ --exclude-subdir \
      && rm cmake-3.12.1-Linux-x86_64.sh \
      && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 60 \
                         --slave /usr/bin/g++ g++ /usr/bin/g++-8 \
      && update-alternatives --config gcc \
      && mkdir build \
      && cd build #\
      #&& cmake -DCMAKE_BUILD_TYPE=Debug .. 
