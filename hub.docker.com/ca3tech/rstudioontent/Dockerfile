FROM ubuntu:14.04
MAINTAINER Corey Scott <slogic01@gmail.com>

ENV INSTDIR mybitcoin

# install dependencies
RUN apt-get update \
 && apt-get install -y software-properties-common \
 && add-apt-repository -y ppa:bitcoin/bitcoin \
 && apt-get update \
 && apt-get install -y libdb4.8-dev \
    libdb4.8++-dev \
    build-essential \
    libtool \
    autotools-dev \
    automake \
    pkg-config \
    libssl-dev \
    libevent-dev \
    bsdmainutils \
    python3 \
    libboost-system-dev \
    libboost-filesystem-dev \
    libboost-chrono-dev \
    libboost-program-options-dev \
    libboost-test-dev \
    libboost-thread-dev \
    git

# download and compile
RUN mkdir $INSTDIR && cd $INSTDIR && git clone https://github.com/bitcoin/bitcoin.git . && ./autogen.sh && ./configure CXXFLAGS="--param ggc-min-expand=1 --param ggc-min-heapsize=32768" && make && make install

EXPOSE 8332 8333 18332 18333 18444

CMD ["test_bitcoin"]

