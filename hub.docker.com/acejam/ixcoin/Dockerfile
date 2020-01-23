FROM ubuntu:16.04
MAINTAINER Joshua Noble <acejam@gmail.com>

ENV RPC_USER ixcoinrpc
ENV RPC_PASS P@ssw0rd
ENV RPC_ALLOW_IP 127.0.0.1
ENV MAX_CONNECTIONS 15
ENV RPC_PORT 8338
ENV PORT 8337
WORKDIR /app

RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:bitcoin/bitcoin

RUN apt-get update && apt-get install -y \
      build-essential \
      git \
      libboost-filesystem-dev \
      libboost-program-options-dev \
      libboost-system-dev \
      libboost-test-dev \
      libboost-thread-dev \
      libdb4.8-dev \
      libdb4.8++-dev \
      libssl-dev \
      libglib2.0-dev && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/ixcoin/ixcoin.git && \
    cd ixcoin/src && \
    make -f makefile.unix ixcoind && \
    mv ixcoind /usr/bin/ixcoind && \
    mkdir -p /data/ixcoin

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 8337 8338
VOLUME ["/data/ixcoin"]
CMD ["/usr/bin/ixcoind", "-datadir=/data/ixcoin", "-printtoconsole"]
