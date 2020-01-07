FROM phusion/baseimage:0.10.0
MAINTAINER Julian Haupt <jh@coinctrl.com>

RUN apt-get update -qq && \
    apt-get install -y software-properties-common build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils yasm \
    libboost-all-dev libzmq3-dev curl wget && \
    add-apt-repository ppa:bitcoin/bitcoin && \
    apt-get update && \
    apt-get install -y libdb4.8-dev libdb4.8++-dev && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV     TERM xterm

ENV     BITCOIN_VERSION 0.15.1

ENV     BITCOIN_USER_ID         1000
ENV     BITCOIN_USER            bitcoin

ENV     BITCOIN_GROUP_ID        1000
ENV     BITCOIN_GROUP           bitcoin

ENV     BITCOIN_HOME /var/lib/bitcoin
ENV     BITCOIND_PARAMS ""

RUN     groupadd -g ${BITCOIN_GROUP_ID} ${BITCOIN_GROUP} && \
        useradd -u ${BITCOIN_USER_ID} -g ${BITCOIN_GROUP} -s /bin/false -m -d ${BITCOIN_HOME} ${BITCOIN_USER}

RUN     curl -L --silent -o /tmp/bitcoin.tar.gz https://github.com/bitcoin/bitcoin/archive/v${BITCOIN_VERSION}.tar.gz && \
        tar -xvzf /tmp/bitcoin.tar.gz -C /usr/src && \
        rm /tmp/bitcoin.tar.gz && \
        cd /usr/src/bitcoin-${BITCOIN_VERSION} && \
        ./autogen.sh && \
        ./configure --disable-tests && \
        make && make install && \
        rm -r /usr/src/bitcoin-${BITCOIN_VERSION}

VOLUME  ["${BITCOIN_HOME}"]

ADD     etc/ /etc/
ADD     docker-entrypoint.sh /usr/local/sbin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/sbin/docker-entrypoint.sh"]

EXPOSE      8332 8333 18332 18333
# phusion/baseimage docker optimized init script
CMD         ["/sbin/my_init"]
