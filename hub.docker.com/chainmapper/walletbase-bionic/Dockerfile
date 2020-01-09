FROM ubuntu:bionic

RUN apt-get update \
    && apt-get -y upgrade \
	&& export DEBIAN_FRONTEND=noninteractive \
	&& apt-get -y install libboost-system1.65.1 libboost-filesystem1.65.1 libboost-program-options1.65.1 \
	libboost-thread1.65.1 libboost-chrono1.65.1 libdb4.8 libdb4.8++ libssl1.0.0 unzip \
	libevent-2.1-6 libevent-pthreads-2.1-6 software-properties-common wget libzmq5 libminiupnpc10 libcap2 libb2-1 \
    && add-apt-repository ppa:bitcoin/bitcoin \
    && apt-get update \
    && apt-get -y install libdb4.8-dev libdb4.8++-dev unzip