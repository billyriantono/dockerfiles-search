FROM greatbsky/xtraos:latest
MAINTAINER architect.bian
LABEL name="litecoin" license="MIT" build-date="20180906"

ENV VERSION 0.16.0

RUN yum update -y && cd /data/softs && wget https://download.litecoin.org/litecoin-$VERSION/linux/litecoin-$VERSION-x86_64-linux-gnu.tar.gz && tar -zvxf litecoin-$VERSION-x86_64-linux-gnu.tar.gz && install -m 0755 -o root -g root -t /usr/local/bin litecoin-$VERSION/bin/* && rm -rf /data/softs/*

RUN sed -i '$d' /etc/rc.local && echo 'litecoind' >> /etc/rc.local

CMD ["/etc/rc.local"]
