FROM ubuntu:16.04
MAINTAINER Zaki Alam <zaki.alam@gmail.com>

# Update xmrig minimum donate level
ARG DONATE_LEVEL=0
ARG GIT_TAG

WORKDIR /app
USER root

# Update system software and install compiler
RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get install -y gcc-8 g++-8 git build-essential cmake libuv1-dev libmicrohttpd-dev libssl-dev

# Download latest version of xmrig
RUN git clone https://github.com/xmrig/xmrig.git
WORKDIR /app/xmrig
RUN git checkout $GIT_TAG

# Adjust donation level
RUN sed -i -r "s/k([[:alpha:]]*)DonateLevel = [[:digit:]]/k\1DonateLevel = ${DONATE_LEVEL}/g" src/donate.h

# Build xmrig
RUN mkdir build
WORKDIR /app/xmrig/build
RUN cmake .. -DCMAKE_C_COMPILER=gcc-8 -DCMAKE_CXX_COMPILER=g++-8 -DWITH_HTTPD=OFF
RUN make

# Start xmrig
CMD ./xmrig -c $XMRIG_JSON_CONFIG_PATH

