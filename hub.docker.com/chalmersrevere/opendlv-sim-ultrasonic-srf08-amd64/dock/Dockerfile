FROM chainmapper/walletbase-bionic

RUN apt-get update \
    && apt-get -y upgrade \
    && apt-get -y install git build-essential libtool autotools-dev automake \
    pkg-config libssl-dev libevent-dev bsdmainutils libboost-system-dev \
    libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev \
    libboost-test-dev libboost-thread-dev libgmp10-dev \
    g++-mingw-w64-i686 mingw-w64-i686-dev g++-mingw-w64-x86-64 mingw-w64-x86-64-dev curl \
    libcap-dev libseccomp-dev zlib1g-dev libzmq3-dev libb2-dev