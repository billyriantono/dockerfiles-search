########################################################################
# Dockerfile for Haskell on Ubuntu 14.04
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Component:    GHC 7.8.3, Cabal 1.20.0
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/pjan/docker-haskell
# License:      MIT
########################################################################

# pull base image
FROM ubuntu:14.04

# maintainer details
MAINTAINER pjan vandaele "pjan@pjan.io"

# add a post-invoke hook to dpkg which deletes cached deb files
# update the sources.list
# update/dist-upgrade
# clear the caches
RUN \
  echo 'DPkg::Post-Invoke {"/bin/rm -f /var/cache/apt/archives/*.deb || true";};' | tee /etc/apt/apt.conf.d/no-cache && \
  echo "deb http://ap-northeast-1.ec2.archive.ubuntu.com/ubuntu trusty main universe" >> /etc/apt/sources.list && \
  apt-get update -q -y && \
  apt-get dist-upgrade -y && \
  apt-get clean && \
  rm -rf /var/cache/apt/*

# install dependencies
RUN \
  DEBIAN_FRONTEND=noninteractive apt-get install -y -q wget build-essential libgmp3-dev zlib1g-dev libedit2 libglu1-mesa-dev freeglut3 freeglut3-dev

# install GHC
RUN \
  wget -q http://www.haskell.org/ghc/dist/7.8.3/ghc-7.8.3-x86_64-unknown-linux-deb7.tar.bz2 && \
  tar xjf ghc-7.8.3-x86_64-unknown-linux-deb7.tar.bz2 && \
  rm ghc-7.8.3-x86_64-unknown-linux-deb7.tar.bz2 && \
  cd ghc-7.8.3 && \
  ./configure --prefix=/usr/share/haskell/ghc-7.8.3 && \
  make install && \
  cd / && rm -r ghc-7.8.3 && \
  update-alternatives --install "/usr/bin/ghc" "ghc" "/usr/share/haskell/ghc-7.8.3/bin/ghc" 1 && \
  update-alternatives --install "/usr/bin/ghci" "ghci" "/usr/share/haskell/ghc-7.8.3/bin/ghci" 1 && \
  update-alternatives --install "/usr/bin/runghc" "runghc" "/usr/share/haskell/ghc-7.8.3/bin/runghc" 1 && \
  update-alternatives --install "/usr/bin/ghc-pkg" "ghc-pkg" "/usr/share/haskell/ghc-7.8.3/bin/ghc-pkg" 1 && \
  update-alternatives --install "/usr/bin/haddock" "haddock" "/usr/share/haskell/ghc-7.8.3/bin/haddock" 1 && \
  update-alternatives --install "/usr/bin/hp2ps" "hp2ps" "/usr/share/haskell/ghc-7.8.3/bin/hp2ps" 1 && \
  update-alternatives --install "/usr/bin/hsc2hs" "hsc2hs" "/usr/share/haskell/ghc-7.8.3/bin/hsc2hs" 1 && \
  update-alternatives --install "/usr/bin/hpc" "hpc" "/usr/share/haskell/ghc-7.8.3/bin/hpc" 1 && \
  update-alternatives --install "/usr/bin/runhaskell" "runhaskell" "/usr/share/haskell/ghc-7.8.3/bin/runhaskell" 1

# install cabal-install
RUN \
  wget -q http://www.haskell.org/cabal/release/cabal-install-1.20.0.3/cabal-install-1.20.0.3.tar.gz && \
  tar xvf cabal-install-1.20.0.3.tar.gz && \
  rm cabal-install-1.20.0.3.tar.gz && \
  cd cabal-install-1.20.0.3 && ./bootstrap.sh && \
  cd / && rm -r cabal-install-1.20.0.3

ENV PATH /.cabal/bin/:$PATH

# Define a mountable data directory
VOLUME \
  ["/data"]

# Define the working directory
WORKDIR \
  /data

# Define default command
CMD \
  ["/bin/bash"]
