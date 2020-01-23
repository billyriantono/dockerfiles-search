FROM greatbsky/centos7:latest
MAINTAINER architect.bian
LABEL name="bitcoincash" license="MIT" build-date="20180904"

ENV VERSION 0.18.1

RUN yum update -y && cd /data/softs && wget https://download.bitcoinabc.org/$VERSION/linux/bitcoin-abc-$VERSION-x86_64-linux-gnu.tar.gz && tar -zvxf bitcoin-abc-$VERSION-x86_64-linux-gnu.tar.gz && install -m 0755 -o root -g root -t /usr/bin bitcoin-abc-$VERSION/bin/*  && mv bitcoin-abc-$VERSION /data/env/ && echo 'export BCHROOT=/data/env/bitcoin-abc-$VERSION' >> /etc/profile && echo -e 'export PATH=$PATH:$BCHROOT/bin\n' >> /etc/profile && rm -rf /data/softs/*

CMD ["bitcoind"]
