FROM ubuntu:18.04

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils wget

RUN wget --no-check-certificate https://github.com/ethereumproject/go-ethereum/releases/download/v5.5.1/geth-classic-linux-v5.5.1-8a3bc2d.tar.gz
RUN tar -xvzf geth-classic-linux-v5.5.1-8a3bc2d.tar.gz
RUN cp geth /usr/bin/geth-classic

WORKDIR /app

EXPOSE 8545
