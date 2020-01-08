FROM debian:latest
MAINTAINER Valerie Parham-Thompson <valerie@tortugatech.com>

RUN apt-get update && \
        apt-get -y install curl

RUN curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | bash

RUN apt-get -y install sysbench git make gcc unzip wget lua5.1 lua5.1-dev vim && \
        apt-get clean

RUN wget https://luarocks.org/releases/luarocks-2.4.3.tar.gz && tar zxpf luarocks-2.4.3.tar.gz && cd luarocks-2.4.3 && ./configure && make bootstrap

RUN luarocks install lua-cassandra --local
RUN luarocks install luasocket --local