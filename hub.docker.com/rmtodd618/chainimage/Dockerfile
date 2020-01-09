FROM ubuntu:16.04
MAINTAINER Ryan Todd
RUN apt-get update
RUN apt-get install -y automake libdb++-dev build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libminiupnpc-dev git software-properties-common python-software-properties g++
RUN add-apt-repository ppa:bitcoin/bitcoin -y
RUN apt-get update
RUN apt-get install libdb4.8-dev bsdmainutils libdb4.8++-dev -y
RUN git clone https://github.com/chaincoin/chaincoin.git
RUN cd chaincoin && ./autogen.sh && ./configure -without-gui && make && make install
RUN mkdir /root/.chaincoin/
WORKDIR chaincoin/src/
ENTRYPOINT "chaincoind"