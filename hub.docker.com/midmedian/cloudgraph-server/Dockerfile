FROM ubuntu:latest

MAINTAINER Ilya Babkin <ilya.babkin1@mail.ru>

ENTRYPOINT ["/bin/bash"]

RUN \
apt-get update && \
apt-get -y upgrade && \
apt-get -y install bash gcc g++ build-essential clang \
qt5-default && \
apt-get -y autoremove && \
apt-get -y autoclean && \
apt-get -y clean && \
rm -rf /var/lib/apt/lists/*

ADD . /app

WORKDIR /app

RUN qmake cloudgraph-server.pro && \
make

RUN groupadd -r sample && useradd -r -g sample sample
USER sample

EXPOSE 3141/tcp

ENTRYPOINT ["/app/cloudgraph-server"]
