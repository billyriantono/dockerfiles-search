FROM ubuntu:xenial

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install libboost-all-dev libdb4.8 libdb4.8++ libssl1.0.0 \
    && apt-get -y install git build-essential libtool autotools-dev automake \
    pkg-config libssl-dev libevent-dev bsdmainutils software-properties-common libgmp3-dev \
    libseccomp-dev libcap-dev libminiupnpc-dev libprotobuf-dev protobuf-compiler \
    && add-apt-repository ppa:bitcoin/bitcoin \
    && apt-get update \
    && apt-get -y install libdb4.8-dev libdb4.8++-dev unzip zlib1g-dev libz-dev

RUN git clone --recurse-submodules https://github.com/vergecurrency/VERGE.git \
    && cd VERGE \
    && chmod +x autogen.sh \
    && ./autogen.sh && ./configure \
    && make \
    && make install \
    && cd / && rm -rf VERGE

ENV HOME /root

#rpc and mn port
EXPOSE 21102 20102

CMD VERGEd