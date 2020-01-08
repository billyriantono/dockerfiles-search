FROM ubuntu:16.04

RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y nano wget python-pip pkg-config zlib1g-dev gcc glib-2.0 libglib2.0-dev libsdl1.2-dev libaio-dev libcap-dev libattr1-dev libpixman-1-dev libfdt-dev wget git unzip libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev libboost-all-dev unzip libminiupnpc-dev python-virtualenv build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils libdb++-dev libcrypto++-dev libqrencode-dev libgmp-dev libgmp3-dev autoconf autogen
RUN apt-get install -y libminiupnpc-dev libzmq3-dev libevent-pthreads-2.0-5

RUN apt-get -y install software-properties-common && add-apt-repository ppa:bitcoin/bitcoin
RUN apt-get update
RUN apt-get -y install libdb4.8-dev libdb4.8++-dev

WORKDIR /root/
ADD source/ /root/source/
