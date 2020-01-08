FROM ubuntu:14.04
MAINTAINER kotik <obrbkru@apriorit.com>

#install custom packages
RUN apt-get -q update

#install libdb4.8
#--software-properties-common for adding add-apt-repository
RUN apt-get install -y software-properties-common && add-apt-repository -y ppa:bitcoin/bitcoin && apt-get update
RUN apt-get install -y libdb4.8-dev libdb4.8++-dev

#install dependencies
RUN apt-get install -y build-essential libtool autotools-dev autoconf libssl-dev pkg-config libevent-dev automake
RUN apt-get install -y libboost-all-dev
RUN apt-get install -y libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

#configure
#install bsdmainutils for fixing "hexdump is required for tests"
RUN apt-get install -y bsdmainutils 
#folder Source must be mounted

#run example:
#sudo docker run -d -t -v ~/Source:/Source apriorit/build-deviant-coin\
#  "bash -c cd /Source && chmod +x autogen.sh && ./autogen.sh && ./configure &&\
#  chmod +x ./src/leveldb/build_detect_platform && chmod +x ./share/genbuild.sh && make"
