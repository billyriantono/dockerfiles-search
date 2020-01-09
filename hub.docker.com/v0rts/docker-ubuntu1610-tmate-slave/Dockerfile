FROM ubuntu:16.10
MAINTAINER Chad Sailer

# Install packages
RUN apt-get update \
    && apt-get install -y \
       git-core build-essential pkg-config libtool libevent-dev libncurses-dev zlib1g-dev automake libssh-dev cmake ruby wget\
    && apt-get clean

Run mkdir -p /root/msgpack \
    && cd /root/msgpack \
    &&  wget https://github.com/msgpack/msgpack-c/releases/download/cpp-1.3.0/msgpack-1.3.0.tar.gz \
    && tar -xzf msgpack-1.3.0.tar.gz \
    && cd msgpack-1.3.0 \
    && ./configure --prefix=/usr && make && make install

RUN cd /root \
    && git clone https://github.com/tmate-io/tmate-slave.git \
    && cd tmate-slave \
    && ./create_keys.sh > keyInfo \
    && ./autogen.sh && ./configure && make

RUN locale-gen en_US.UTF-8
