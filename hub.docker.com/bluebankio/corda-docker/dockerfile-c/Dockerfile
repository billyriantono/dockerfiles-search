# Build via docker:
# docker build --build-arg cores=8 -t blocknetdx/wgr:latest .

FROM ubuntu:xenial

ARG cores=1
ENV ecores=$cores

RUN apt update \
  && apt install -y --no-install-recommends \
     software-properties-common \
     ca-certificates \
     wget curl git python vim \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN add-apt-repository ppa:bitcoin/bitcoin \
  && apt update \
  && apt install -y --no-install-recommends \
     curl build-essential libtool autotools-dev automake \
     python3 bsdmainutils cmake libevent-dev autoconf automake \
     pkg-config libssl-dev libboost-system-dev libboost-filesystem-dev \
     libboost-chrono-dev libboost-program-options-dev libboost-test-dev \
     libboost-thread-dev libdb4.8-dev libdb4.8++-dev libgmp-dev \
     libminiupnpc-dev libzmq3-dev \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Build source
RUN mkdir -p /opt/wagerr \
  && mkdir -p /opt/blockchain/config \
  && mkdir -p /opt/blockchain/data \
  && ln -s /opt/blockchain/config /root/.wagerr \
  && cd /opt/wagerr \
  && git clone --depth 1 --branch v3.1.0 https://github.com/wagerr/wagerr wagerr \
  && cd /opt/wagerr/wagerr/ \
  && cd depends \
  && make -j$ecores NO_QT=1 \
  && cd .. \
  && chmod +x ./autogen.sh \
  && ./autogen.sh \
  && ./configure --with-gui=no --enable-hardening --prefix=`pwd`/depends/x86_64-pc-linux-gnu \
  && make -j$ecores \
  && make install \
  && cp /opt/wagerr/wagerr/src/wagerrd /opt/blockchain/wagerrd \
  && rm -rf /opt/wagerr/

# Write default wagerr.conf (can be overridden on commandline)
RUN echo "datadir=/opt/blockchain/data  \n\
                                        \n\
dbcache=256                             \n\
maxmempool=512                          \n\
                                        \n\
port=55002                               \n\
rpcport=55003                          \n\
                                        \n\
                                        \n\
listen=1                                \n\
server=1                                \n\
maxconnections=16                       \n\
logtimestamps=1                         \n\
logips=1                                \n\
                                        \n\
rpcallowip=127.0.0.1                    \n\
rpctimeout=15                           \n\
rpcclienttimeout=15                     \n" > /opt/blockchain/config/wagerr.conf

WORKDIR /opt/blockchain/
VOLUME ["/opt/blockchain/config", "/opt/blockchain/data"]

# Port, RPC, Test Port, Test RPC
EXPOSE 55002 55003  18332  19332

CMD ["/opt/blockchain/wagerrd", "-daemon=0"]