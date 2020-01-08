FROM ubuntu:14.04
MAINTAINER renzhi renzhi828@163.com
RUN sudo apt-get update &&\
                       apt-get install -y \
                       linux-tools-generic libbz2-dev python-dev scons\
                       libtool liblzma-dev libblas-dev make automake \
                       ccache ant openjdk-7-jdk libcppunit-dev doxygen \
                       libcrypto++-dev libACE-dev gfortran liblapack-dev \
                       libevent-dev libssh2-1-dev libicu-dev libv8-dev \
                       g++ google-perftools libgoogle-perftools-dev \
                       zlib1g-dev git pkg-config valgrind autoconf \
                       libcurl4-openssl-dev cmake libsigc++-2.0-dev \
                       unzip &&\
                       apt-get clean
ENV HOME="/home/rtbkit"
RUN sudo useradd -m rtbkit &&\
         mkdir -p $HOME/local/bin &&\
         mkdir -p $HOME/local/lib/pkgconfig/ &&\
         mkdir -p $HOME/local/lib/pkg-config/
ENV PATH="$HOME/local/bin:$PATH" \
    LD_LIBRARY_PATH="$HOME/local/lib:$LD_LIBRARY_PATH" \
    PKG_CONFIG_PATH="$HOME/local/lib/pkgconfig/:$HOME/local/lib/pkg-config/"
USER rtbkit
