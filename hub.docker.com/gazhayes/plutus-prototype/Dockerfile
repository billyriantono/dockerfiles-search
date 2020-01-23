FROM ubuntu:16.04

RUN apt-get update &&\
    apt-get install -y git curl bzip2 libssl-dev software-properties-common python3-software-properties &&\
    add-apt-repository -y ppa:hvr/ghc &&\
    apt-get update &&\
    curl -sSL https://get.haskellstack.org/ | sh &&\
    useradd -ms /bin/bash plutus &&\
    su - plutus -c 'git clone https://github.com/input-output-hk/plutus-prototype.git /home/plutus/plutus-proto' &&\
    apt-get install -y cabal-install 

USER plutus
ENV USER plutus

WORKDIR /home/plutus/plutus-proto
RUN cabal update &&\
    stack build
