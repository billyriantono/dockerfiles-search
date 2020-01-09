FROM ubuntu:14.04

RUN sudo apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
RUN sudo add-apt-repository ppa:bitcoin/bitcoin
RUN sudo apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libdb4.8-dev libdb4.8++-dev

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libboost-all-dev

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libminiupnpc-dev
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libzmq3-dev
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget g++
