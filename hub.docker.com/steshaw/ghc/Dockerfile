from i386/debian:jessie

workdir /work
run \
    echo 'deb http://httpredir.debian.org/debian jessie-backports main' >>/etc/apt/sources.list && \
    apt-get update && \
    apt-get -t jessie-backports install -y ghc alex happy cabal-install
run apt-get install -y git make pkg-config zlib1g-dev libffi-dev
run ghc --version
run cabal --version
run git --version
run pkg-config --version
