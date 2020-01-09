FROM amazonlinux:latest

ENV LANG C.UTF-8

# Ruby version
ARG VERSION_MAJOR="2"
ARG VERSION_MINOR="6"
ARG VERSION_BUILD="3"
ARG VERSION_RELEASE_TYPE=""

WORKDIR /root

RUN yum update -y && \
    yum install -y \
      gcc \
      gzip \
      make \
      tar && \
    yum clean all

RUN curl -o ruby-${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_BUILD}${VERSION_RELASE_TYPE}.tar.gz \
  https://cache.ruby-lang.org/pub/ruby/${VERSION_MAJOR}.${VERSION_MINOR}/ruby-${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_BUILD}${VERSION_RELASE_TYPE}.tar.gz

RUN tar xf ruby-${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_BUILD}${VERSION_RELASE_TYPE}.tar.gz
RUN cd ruby-${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_BUILD}${VERSION_RELASE_TYPE} && \
  ./configure \
    --prefix=/usr/local && \
  make && \
  make install

RUN rm -rf ruby-*

RUN ruby -v

