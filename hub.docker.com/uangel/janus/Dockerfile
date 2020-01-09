FROM centos:7

RUN yum install -y epel-release && \
    yum update -y && \
    yum install -y deltarpm && \
    yum install -y \
        openssh-server \
        sudo \
        which \
        file \
        curl \
        zip unzip \
        wget && \
    yum install -y \
        libmicrohttpd-devel \
        jansson-devel \
        libnice-devel \
        openssl-devel \
        glib2-devel \
        opus-devel \
        libogg-devel \
        pkgconfig \
        gengetopt \
        libtool \
        autoconf \
        automake \
        make \
        gcc gcc-c++ \
        git \
        cmake

#########################
# Prepare Directory

RUN mkdir /share && \
    mkdir /janus && \
    mkdir /janus/bin && \
    mkdir -p /janus/lib/pkgconfig

ENV JANUS_HOME=/janus \
    PATH=/janus/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    PKG_CONFIG_PATH=/janus/lib/pkgconfig:/usr/lib64/pkgconfig:/usr/lib/pkgconfig \
    LD_LIBRARY_PATH=/janus/lib:/usr/lib64:/usr/lib

#
# sofia-sip
#
RUN wget -O /share/sofia-sip-1.12.11.tar.gz https://sourceforge.net/projects/sofia-sip/files/sofia-sip/1.12.11/sofia-sip-1.12.11.tar.gz/download &&\
    cd /share && tar zxf sofia-sip-1.12.11.tar.gz && cd sofia-sip-1.12.11 &&\
    ./configure --prefix=$JANUS_HOME CFLAGS=-fno-aggressive-loop-optimizations &&\
    make && make install &&\

#
# libsrtp 1.5.4 upgrade
#
    wget -O /share/libsrtp-v1.5.4.zip https://github.com/cisco/libsrtp/archive/v1.5.4.zip &&\
    cd /share && unzip libsrtp-v1.5.4.zip && cd libsrtp-1.5.4 &&\
    ./configure --prefix=$JANUS_HOME --enable-openssl &&\
    make && make shared_library && make install && \

#
# usrsctp - Data Channel Support
#
    cd /share && \
    git clone https://github.com/sctplab/usrsctp && \
    cd usrsctp && \
    ./bootstrap && \
    ./configure --prefix=$JANUS_HOME && make && make install && \

#
# libwebsocket
#  - alternative git repository: https://github.com/warmcat/libwebsockets.git
#
    cd /share && \
    git clone git://git.libwebsockets.org/libwebsockets && \
    cd libwebsockets && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_INSTALL_PREFIX:PATH=$JANUS_HOME -DCMAKE_C_FLAGS="-fpic" .. && \
    make && make install

#
# Janus
#
RUN cd /share &&\
    git clone https://github.com/meetecho/janus-gateway.git &&\
    cd /share/janus-gateway &&\
    sh autogen.sh &&\
    ./configure --prefix=$JANUS_HOME --disable-rabbitmq --disable-docs LDFLAGS=-L$JANUS_HOME/lib CFLAGS=-I$JANUS_HOME/include &&\
    make &&\
    make install &&\
    make configs
