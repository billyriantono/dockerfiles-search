FROM ubuntu:18.04

LABEL \
	maintainer="juliendequaire"

# update
RUN apt-get update -qq

# install basic
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    ssh \
    git \
    make \
    cmake \
    clang \
    libgtest-dev

# build & install gtest
RUN cd /usr/src/gtest ; cmake . ; make
RUN mv /usr/src/gtest/*.a /usr/lib/

ENV \
    CC="/usr/bin/clang" \
    CXX="/usr/bin/clang++"