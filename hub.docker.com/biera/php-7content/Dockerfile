FROM ubuntu-debootstrap:14.04
MAINTAINER Benno Fünfstück <benno.fuenfstueck@gmail.com>
LABEL Description="This image is used to build a haskell sofwarechallenge 2016 client."

RUN apt-get update
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" >> /etc/apt/apt.conf
RUN apt-get install software-properties-common pkg-config libcairo2-dev libgtk2.0-dev libpango1.0-dev libglib2.0-dev
RUN add-apt-repository ppa:hvr/ghc && apt-get update && apt-get install ghc-7.10.2 cabal-install-1.22 git zlib1g-dev sudo gawk curl
ENV PATH=$PATH:/opt/ghc/7.10.2/bin:/opt/cabal/1.22/bin:$HOME/.cabal/bin

RUN mkdir /build /build/sc16 /build/sclib
WORKDIR /build
ADD https://bitbucket.org/chaosteam/sclib/raw/master/sclib.cabal /build/sclib/sclib.cabal
ADD ./sc16.cabal /build/sc16/sc16.cabal
RUN cabal update
RUN cabal install alex happy gtk2hs-buildtools
RUN cabal install --only-dep --enable-tests --enable-benchmarks ./sclib ./sc16
