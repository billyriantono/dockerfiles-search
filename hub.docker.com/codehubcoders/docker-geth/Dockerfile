FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive
ENV NODE_ENV production

RUN apt-get update && \
    apt-get -qq -y upgrade && \
    apt-get install -qq -y software-properties-common && \
    add-apt-repository -y ppa:ethereum/ethereum
RUN apt-get update -qq && \
    apt-get install -qq -y geth

VOLUME ["/root/.ethereum"]

EXPOSE 8545 30303

CMD [ "geth", "--rpcaddr", "0.0.0.0", "--rpcapi", "'personal,eth,web3'", "--rpc" ]
