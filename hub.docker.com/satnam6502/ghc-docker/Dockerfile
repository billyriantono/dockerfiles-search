FROM ubuntu:14.04
MAINTAINER Darin Morrison <darinmorrison+docker@gmail.com>
MAINTAINER Satnam Singh <satnam6502@gmail.com>

# This image provides a minimal GHC environment using
# GHC version 7.8.3. By default this image will run
# the Haskell interpreter ghci, but this can be overridden e.g.
# to run a shell like bash instead. Lots of code stolen from
# Darin Morrison's Dockerfiles.

## Custom apt-get install options.
ENV OPTS_APT -y --force-yes --no-install-recommends

## add ppa for ubuntu trusty haskell packages
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F6F88286\
 && echo 'deb     http://ppa.launchpad.net/hvr/ghc/ubuntu trusty main' >> /etc/apt/sources.list.d/haskell.list\
 && echo 'deb-src http://ppa.launchpad.net/hvr/ghc/ubuntu trusty main' >> /etc/apt/sources.list.d/haskell.list

## Haskell package versions; can be overriden via context hacks.
ENV VERSION_GHC    7.8.3

# Install GHC dependencies and then ghc-7.8.3
RUN apt-get update && \
    apt-get install ${OPTS_APT} \
      libgmp-dev \
      ghc-7.8.3 && \
    apt-get clean

## Link the binaries into /usr/local/bin
RUN find /opt -maxdepth 3 -name bin -type d\
  -exec sh -c\
    'cd {} && ls .\
      | egrep -v ^.*\-[.[:digit:]]+$\
      | xargs -I % ln -s `pwd`/% /usr/local/bin/%' \;

# Run ghci by default.
CMD ["ghci"]
