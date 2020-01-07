FROM ubuntu:xenial

RUN apt-get update -qq
RUN apt-get upgrade -y -qq
RUN apt-get install -y -qq wget

ENV BITCOIN_VERSION 0.16.1

WORKDIR /root

RUN wget -q https://bitcoincore.org/bin/bitcoin-core-${BITCOIN_VERSION}/bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz
RUN tar -xzf *.tar.gz
RUN rm -rf bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz

RUN cp bitcoin-${BITCOIN_VERSION}/bin/* /bin
RUN mkdir -p /root/.bitcoin

COPY bitcoin.conf /root/.bitcoin/bitcoin.conf

VOLUME ["/root/.bitcoin"]

EXPOSE 8332 8333

CMD ["bitcoind"]