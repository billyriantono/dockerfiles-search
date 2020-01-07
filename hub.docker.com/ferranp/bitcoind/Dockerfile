FROM ubuntu
MAINTAINER Ferran Pegueroles

RUN apt-get update && apt-get install -y software-properties-common

RUN add-apt-repository ppa:bitcoin/bitcoin \
 && apt-get update \
 && apt-get install -y --no-install-recommends bitcoind \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ["/.bitcoin"]

# bitcoind testnet ports
EXPOSE 8332 8333

CMD ["/usr/bin/bitcoind", "-debug", "-server"]
