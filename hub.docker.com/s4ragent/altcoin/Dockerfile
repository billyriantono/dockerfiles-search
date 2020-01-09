FROM ubuntu:16.04
MAINTAINER @s4r_agent

RUN apt-get update -y \
&& apt-get install -y git automake build-essential libcurl4-openssl-dev pkg-config libc6-dev m4 g++-multilib autoconf libtool ncurses-dev unzip git python python-zmq zlib1g-dev wget bsdmainutils curl
#build cpuminer
RUN git clone https://github.com/koto-dev/cpuminer-yescrypt.git
WORKDIR cpuminer-yescrypt
RUN ./autogen.sh \
&& ./configure CFLAGS="-O3" \
&& make \
&& make install

WORKDIR /
RUN git clone https://github.com/koto-dev/koto.git
WORKDIR koto
RUN ./zcutil/fetch-params.sh \
&& ./zcutil/build.sh --disable-rust -j2
