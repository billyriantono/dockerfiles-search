FROM ubuntu:14.04.2
MAINTAINER Mitchell Mebane <mitchell.mebane@gmail.com>

# Basic Ubuntu updates
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get upgrade -y

# Install Ethereum
RUN DEBIAN_FRONTEND=noninteractive apt-get install -qy software-properties-common \
 && add-apt-repository ppa:ethereum/ethereum \
 && add-apt-repository ppa:ethereum/ethereum-qt \
 && apt-get update

ENV ETH_VERSION 0.8.2+28trusty-0ubuntu1
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
 cpp-ethereum=$ETH_VERSION \
 eth=$ETH_VERSION \
 neth=$ETH_VERSION \
 mix=$ETH_VERSION \
 libethereum=$ETH_VERSION \
 libethereum-gui=$ETH_VERSION \
 alethzero=$ETH_VERSION \
 solc=$ETH_VERSION \
 lllc=$ETH_VERSION \
 testeth=$ETH_VERSION

EXPOSE 30303 8080

ENTRYPOINT ["/usr/bin/eth"]
