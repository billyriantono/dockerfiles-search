FROM ubuntu:16.04

MAINTAINER siguernstore@protonmail.com

RUN apt-get update && apt-get install -y \
	automake libdb++-dev build-essential \
	libtool autotools-dev autoconf pkg-config \
	libssl-dev libboost-all-dev libminiupnpc-dev \
	git software-properties-common \
	python-software-properties g++

RUN cd /root && git clone https://github.com/copicogithub1/copico.git &&\
    cd ./copico && cd ./src  && make -f makefile.unix && \
    cd /root/copico/src && cp ./copicod /root/

WORKDIR /root

ENTRYPOINT ["./copicod"]

