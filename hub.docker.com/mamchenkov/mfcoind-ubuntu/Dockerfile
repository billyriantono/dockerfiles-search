FROM ubuntu:16.04

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="MFCoind daemon" \
    org.label-schema.vendor="Alexander Mamchenkov" \
    org.label-schema.livence="MIT" \
    org.label-schema.build-data="20180702"

ENV RPCUSER MFCoinrpc
ENV RPCPASS MFCoinrpcPass

MAINTAINER Alexander Mamchenkov <mamtchenkov@gmail.com>

RUN apt-get update -y \
    && apt-get install -y software-properties-common python-software-properties \
    && add-apt-repository -y ppa:bitcoin/bitcoin \
    && apt-get update -y \
    && apt-get install -y build-essential \
        libssl-dev \
        libdb4.8-dev \
        libdb4.8++-dev \
        libboost1.58-dev \
        libboost1.58-all-dev \
        libminiupnpc-dev \
        git \
        wget \
    && apt-get clean \
    && git clone https://github.com/MFrcoin/MFCoin.git \
    && cd MFCoin/src \
    && make USE_UPNP=0 USE_IPV6=0 -f makefile.unix \
    && mv MFCoind /usr/local/bin/ \
    && cd ../../ \
    && rm MFCoin/ -rf

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

EXPOSE 22823
EXPOSE 22824

CMD ["/usr/local/bin/entrypoint.sh"]
