FROM nvidia/cuda:10.1-base

RUN apt-get -y update && \
    apt-get -y install wget xz-utils

ENV ETH_VERSION=15.5.3-747d98e

RUN wget https://www.bminercontent.com/releases/bminer-v${ETH_VERSION}-amd64.tar.xz && \
    xz -d bminer-v${ETH_VERSION}-amd64.tar.xz && \
    tar xf bminer-v${ETH_VERSION}-amd64.tar --strip-components=1 -C /usr/local/bin && \
    rm -f bminer-v${ETH_VERSION}-amd64.tar
