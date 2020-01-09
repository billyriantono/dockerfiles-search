FROM ubuntu:trusty

ENV IOTIVITY_VERSION 1.2.1_with_bridging

# params that can be overridden at build time

ARG SECURED
ENV SECURED ${SECURED:-1}

ARG RELEASE
ENV RELEASE ${RELEASE:-true}

ARG LOGGING
ENV LOGGING ${LOGGING:-true}

ARG PREFIX
ENV PREFIX ${PREFIX:-/usr}

# Based on instructions on iotivity/Readme.scons.txt

# Install build tools
RUN apt-get -yqq update && apt-get install -yqq \
      git-core \
      scons \
      ssh \
      build-essential \
      g++ \
      doxygen \
      valgrind \
      subversion \
# Install external libraries
      libboost-dev \
      libboost-program-options-dev \
      libboost-thread-dev \
      uuid-dev \
      libssl-dev \
      libtool \
      libglib2.0-dev \
      libsqlite3-dev \
# Install other required packaes
      apt-utils \
      libcurl4-openssl-dev \
      unzip \
      curl \
# extra
      sudo \
      vim \
      wget \
      less \
      python \
      python-pip \
      pkg-config \
# Cleanup
    && rm -rf /var/lib/apt/lists/*

RUN	useradd -m builder && \
	echo 'builder ALL=NOPASSWD: ALL' > /etc/sudoers.d/builder
USER builder
WORKDIR  /home/builder

# Download and build iotivity C/C++ libs and examples
RUN [ "x${RELEASE}" = "xtrue" ] && branch='release' || branch='debug' && \
    git clone https://gerrit.iotivity.org/gerrit/p/iotivity.git --branch ${IOTIVITY_VERSION} && \
    cd iotivity && \
      git clone https://github.com/01org/tinycbor.git extlibs/tinycbor/tinycbor && \
      git clone https://github.com/ARMmbed/mbedtls.git extlibs/mbedtls/mbedtls
      
# RUN   scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} --prefix=${PREFIX} 
#      sudo scons SECURED=${SECURED} RELEASE=${RELEASE} LOGGING=${LOGGING} install --prefix=${PREFIX} && \
