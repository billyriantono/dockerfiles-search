FROM ubuntu:13.10
RUN sudo apt-get update -y && sudo apt-get upgrade -y
RUN sudo apt-get install -y build-essential libgmp-dev libgmp3-dev libcrypto++-dev \
  git cmake libboost1.53-all-dev automake libtool libleveldb-dev yasm unzip libminiupnpc-dev \
  qtbase5-dev qt5-default wget git-arch
RUN mkdir -p /source/cryptopp562
RUN cd /source/cryptopp562 && wget http://www.cryptopp.com/cryptopp562.zip && unzip cryptopp562.zip && make
RUN git clone https://github.com/ethereum/cpp-ethereum /source/cpp-ethereum
RUN mkdir /source/cpp-ethereum-build
RUN cd /source/cpp-ethereum-build && cmake ../cpp-ethereum -DCMAKE_BUILD_TYPE=Release -DHEADLESS=1 && make
