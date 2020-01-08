FROM ubuntu:16.04
MAINTAINER Johann Tanzer <mail@johanntanzer.at>


RUN apt-get update -y && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y git \
 build-essential libssl-dev libboost-all-dev libdb5.3 libdb5.3-dev libdb5.3++-dev libtool automake libevent-dev bsdmainutils \
 git ntp make g++ gcc autoconf cpp ngrep iftop sysstat autotools-dev pkg-config libminiupnpc-dev libzmq3-dev \
 libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev
RUN git clone https://github.com/groestlcoin/groestlcoin
WORKDIR groestlcoin
RUN ./autogen.sh && ./configure && make && make install
RUN chmod +x /groestlcoin/src/groestlcoind

ENTRYPOINT ["/groestlcoin/src/groestlcoind"]
