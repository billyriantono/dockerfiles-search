FROM ubuntu:14.04
MAINTAINER Satnam Singh <satnam6502@gmail.com>

# A basic install of the Haskell Platform 2014.2.0.0 on Ubuntu 14.04.

# Much inspiration from the Dockerfiles:
#   zsol/haskell-platform-2014.2.0.0
#   alanz/haskell-platform-2013.2-deb64
#   darinmorrison/haskell

# Install supporting componets.
# Fetch and install the Haskell Platform.
RUN apt-get update && \
    apt-get install -y curl libgmp3-dev zlib1g-dev && \
    cd / && \
    curl -O http://www.haskell.org/platform/download/2014.2.0.0/haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz && \
    tar xf haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz && \
    /usr/local/haskell/ghc-7.8.3-x86_64/bin/activate-hs && \
    rm /haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz && \
    cabal update && cabal install --global cabal-install && \
    apt-get clean

# By default, run the Haskell interpreter ghci.
CMD ["ghci"]

