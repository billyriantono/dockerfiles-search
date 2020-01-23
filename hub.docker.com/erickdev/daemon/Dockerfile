FROM ubuntu:xenial
MAINTAINER Erick DEV ARTWORK <ericksantpeterberg@outlook.com>

RUN apt-get update \
     && apt-get install wget -y

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y --no-install-recommends \
                       git \
                       build-essential \
                       libtool \
                       autotools-dev \
                       automake \
                       pkg-config \
                       libssl-dev \
                       libevent-dev \
                       bsdmainutils \
                       libboost-system-dev \
                       libboost-filesystem-dev \
                       libboost-chrono-dev \
                       libboost-program-options-dev \
                       libboost-test-dev \
                       libboost-thread-dev \
                       software-properties-common \
                       libminiupnpc-dev \
                       libzmq3-dev \
                       libqt4-dev libprotobuf-dev protobuf-compiler\
                       python3 \
                       libboost-thread-dev libboost-dev libevent-1.4-2 \
                       libqrencode-dev libminiupnpc-dev git \
                       && git clone https://github.com/erickdevartworks/core-test-1.0.0.git /home/ubuntu/core-test-1.0.0
WORKDIR /home/ubuntu/core-test-1.0.0

RUN tar -zxvf core-test-1.0.0.tar.gz \
    && strip core-test-1.0.0/shitcoind core-test-1.0.0/shitcoin-cli core-test-1.0.0/shitcoin-tx \
    && mv core-test-1.0.0/shitcoind /usr/local/bin/ \
    && mv core-test-1.0.0/shitcoin-cli /usr/local/bin/ \
    && mv core-test-1.0.0/shitcoin-tx /usr/local/bin/
EXPOSE 4280 4280 4282 4282

RUN mkdir -p ~/.Shitcoin \
    && echo "rpcuser=eriksfilipovs" >> ~/.Shitcoin/shitcoin.conf \
    && echo "rpcpassword=shitcoinether11" >> ~/.Shitcoin/shitcoin.conf \
    && echo "rpcport=4281" >> ~/.Shitcoin/shitcoin.conf
    
VOLUME [ "/data" ]

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT [ "/docker-entrypoint.sh" ]
ENV SHITCOIN_DBCACHE=400

CMD [ "shitcoind", "--help" ]
