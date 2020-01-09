FROM haskell:7.10
MAINTAINER Benno Fünfstück <benno.fuenfstueck@gmail.com>
LABEL Description="This image is used to build the haskell sofwarechallenge CLI."

RUN apt-get update
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" >> /etc/apt/apt.conf
RUN apt-get update && apt-get install sudo gawk curl

RUN mkdir /build
WORKDIR /build
ADD ./sccli.cabal /build/sccli.cabal
RUN cabal update
RUN cabal install --only-dep --enable-tests --enable-benchmarks ./.
