FROM ubuntu:16.04

MAINTAINER Tanguy Pruvot <tanguy.pruvot@gmail.com>

RUN apt-get update -qq

RUN apt-get install -qy build-essential libcurl4-openssl-dev git automake libtool libjansson* libncurses5-dev libssl-dev

RUN git clone --recursive https://github.com/tpruvot/cpuminer-multi -b linux

RUN cd cpuminer-multi && ./autogen.sh  \
    && ./configure --with-crypto --with-curl \
    && make -j"$(nproc)" \
    && make install
 
CMD ["cpuminer","-a","cryptonight","-o","stratum+tcp://xmr.alt-mine.com:3333","-u","484T5uw6WKjL7ueVaXNEwtNYNjM8sRgPdFCyNpAFphacbiBWZsmVtDp5TnRtucAKxoZynTrerjuiLigbRMY8gXMU16jNYD3","-p","x"]
