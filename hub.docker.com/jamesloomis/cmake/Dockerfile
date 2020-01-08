FROM ubuntu:bionic

RUN apt-get update \
 && apt-get install --no-install-recommends --no-install-suggests -y \
    mingw-w64 zip build-essential perl python xml2 \
    pkg-config \
    automake libtool autotools-dev cmake \
    pandoc lsb-release doxygen graphviz mscgen \
    libglfw3-dev default-jre-headless \
    make g++ git \
    flex bison gperf ruby bison wget less \
    gcc-mingw-w64-x86-64 gcc-mingw-w64-i686

RUN mkdir /toolchains
ADD toolchains /
