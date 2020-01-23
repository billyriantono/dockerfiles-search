FROM ubuntu:18.04 as builder

LABEL author="buzzkillb"

RUN apt-get update && apt-get install -y \
    git \
    wget \
    unzip \
    automake \
    autotools-dev \
    bsdmainutils \
    build-essential \
    libboost-all-dev \
    libqrencode-dev \
    libminiupnpc-dev \
    libevent-dev \
    libssl-dev \
    pkg-config \
    python3 \
    autogen \
    automake \
    libtool \
    make \
    software-properties-common \
    && rm -rf /var/lib/apt/lists/*

RUN add-apt-repository ppa:bitcoin/bitcoin -y && \
    apt-get update && \
    apt-get install --yes libdb4.8-dev libdb4.8++-dev

RUN git clone https://github.com/volta-im/volta-core && \
    cd volta-core && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install

RUN mkdir -p /data

VOLUME ["/data"]

EXPOSE 14143

ENTRYPOINT ["voltad", "--datadir=/data", "--printtoconsole"]
