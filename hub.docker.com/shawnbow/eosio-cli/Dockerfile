FROM ubuntu:18.04
MAINTAINER Shawn Bow <shawnbow81@gmail.com>

RUN apt-get update
RUN apt-get install -y wget

RUN wget https://github.com/eosio/eos/releases/download/v1.8.8/eosio_1.8.8-1-ubuntu-18.04_amd64.deb
RUN apt install -y ./eosio_1.8.8-1-ubuntu-18.04_amd64.deb
RUN rm -f ./eosio_1.8.8-1-ubuntu-18.04_amd64.deb

RUN wget https://github.com/eosio/eosio.cdt/releases/download/v1.6.3/eosio.cdt_1.6.3-1-ubuntu-18.04_amd64.deb
RUN apt install -y ./eosio.cdt_1.6.3-1-ubuntu-18.04_amd64.deb
RUN rm -f ./eosio.cdt_1.6.3-1-ubuntu-18.04_amd64.deb

