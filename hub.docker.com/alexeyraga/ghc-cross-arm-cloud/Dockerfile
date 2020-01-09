# mount the Haskell source code into /home/ghc
#
#    docker run --rm -it --privileged -v `pwd`:/home/ghc alexeyraga/ghc-cross-arm-cloud /bin/bash
#

FROM alexeyraga/ghc-cross-arm:latest
MAINTAINER Alexey Raga

## disable prompts from apt
ENV DEBIAN_FRONTEND noninteractive

RUN cabal update

RUN cabal-arm install "data-accessor" 
RUN cabal-arm install "text" 
RUN cabal-arm install "rank1dynamic" 
RUN cabal-arm install "random" 
RUN cabal-arm install "hashable" 
RUN cabal-arm install "network-transport" 
RUN cabal-arm install "transformers" 
RUN cabal-arm install "mtl" 
RUN cabal-arm install "stm" 
RUN cabal-arm install "syb" 
RUN cabal-arm install "distributed-static" 
RUN cabal-arm install "distributed-process" 
RUN cabal-arm install "network"
RUN cabal-arm install "network-transport-tcp"
