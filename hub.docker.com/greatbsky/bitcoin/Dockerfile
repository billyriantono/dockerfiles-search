FROM greatbsky/centos7:latest
MAINTAINER architect.bian
LABEL name="bitcoin" license="MIT" build-date="20181010"

ENV VERSION 0.17.0

RUN yum update -y && cd /data/softs && wget https://bitcoincore.org/bin/bitcoin-core-$VERSION/bitcoin-$VERSION-x86_64-linux-gnu.tar.gz && tar -zvxf bitcoin-$VERSION-x86_64-linux-gnu.tar.gz && install -m 0755 -o root -g root -t /usr/bin bitcoin-$VERSION/bin/* && rm -rf /data/softs/*

CMD ["bitcoind"]
