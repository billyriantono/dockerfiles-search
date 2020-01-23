FROM ubuntu:18.04

RUN apt-get update

RUN apt-get -y install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils \
    software-properties-common libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev

RUN add-apt-repository ppa:bitcoin/bitcoin

RUN apt-get update

RUN apt-get -y install libdb4.8-dev libdb4.8++-dev

RUN mkdir /build/

WORKDIR /build


