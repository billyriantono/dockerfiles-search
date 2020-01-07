FROM monami0ya/docker-baseimage:14.04
MAINTAINER <info@monaco-ex.org>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-add-repository ppa:bitcoin/bitcoin
RUN apt-get update
RUN apt-get install -y bitcoind

EXPOSE 8332

RUN mkdir /etc/service/bitcoind
ADD bitcoind.sh /etc/service/bitcoind/run

RUN useradd -ms /bin/bash bitcoin

USER bitcoin
RUN mkdir /home/bitcoin/.bitcoin
VOLUME /home/bitcoin/.bitcoin

ENV RPCUSER=bitcoin
ENV RPCPASSWORD=bitcoinpass
ENV RPCALLOWIP="255.255.255.255/0"

USER root
CMD ["/sbin/my_init"]
