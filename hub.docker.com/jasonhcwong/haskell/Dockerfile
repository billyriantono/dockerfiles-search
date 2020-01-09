FROM ubuntu:14.04

ENV LANG=C.UTF-8

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:hvr/ghc \
    && apt-get update \
    && apt-get install -y cabal-install-1.22 ghc-7.10.3 \
    && rm -rf /var/lib/apt/lists/*

ENV PATH /root/.cabal/bin:/opt/cabal/1.22/bin:/opt/ghc/7.10.3/bin:$PATH


CMD ["ghci"]

