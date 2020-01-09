FROM debian:stretch
MAINTAINER Samuel Tardieu <sam@rfc1149.net>
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qq update
RUN apt-get -y dist-upgrade
RUN apt-get --no-install-recommends -y install \
      build-essential ca-certificates clang-4.0 g++ \
      ccache autoconf automake libboost-all-dev \
      flex bison valgrind llvm-4.0-dev \
      clang-format-4.0 python3-yaml libtool zlib1g-dev
ENV PATH="/usr/lib/llvm-4.0/bin:$PATH"
