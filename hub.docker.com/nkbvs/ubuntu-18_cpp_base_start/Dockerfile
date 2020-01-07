# Dockerfile - ubuntu 18.04

FROM nkbvs/ubuntu-18_cpp_base:latest

LABEL maintainer="Denis Tulyakov <dtulyakov@gmail.com>"

# Docker Build Arguments
ARG BOOST_DOT_VERSION="1.66.0"
ARG BOOST_UNDERLINE_VERSION="1_66_0"
ARG LCM_VERSION="1.3.0"
ARG ZEROMQ_VERSION="4.1.6"

#ADD https://dl.bintray.com/boostorg/release/${BOOST_DOT_VERSION}/source/boost_${BOOST_UNDERLINE_VERSION}.tar.gz /tmp/
#ADD https://github.com/jbeder/yaml-cpp/archive/yaml-cpp-${YAML_CPP_VERSION}.tar.gz /tmp
ADD src/boost_${BOOST_UNDERLINE_VERSION}.tar.gz /tmp
ADD src/lcm-${LCM_VERSION}.tar.gz /tmp
ADD src/zeromq-${ZEROMQ_VERSION}.tar.gz /tmp

RUN set -x \
  && cd /tmp/boost_${BOOST_UNDERLINE_VERSION} \
  && ./bootstrap.sh --prefix=/usr/local \
  && ./b2 -j $(nproc) install \
  && cd /tmp/lcm-${LCM_VERSION} \
  && . ./bootstrap.sh \
  && ./configure \
  && make -j $(nproc) install clean \
  && cd /tmp/zeromq-${ZEROMQ_VERSION} \
  && ./configure \
  && make -j $(nproc) install clean \
  && ldconfig \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*
